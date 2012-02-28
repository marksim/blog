---
layout: post
title: Migrating Serialized Columns in Rails
categories: blog
---
I recently switched a serialized column in Rails from one type (Hash) to another (OpenStruct) and ran into a little problem when I tried to migrate, namely, that loading the model threw a SerializationTypeMismatch error.  Hmm... how am I going to get at the base YAML and translate all of these without being brittle?

The answer is to copy the column, nullify it, and the load the raw YAML manually:

<code lang="ruby">
    add_column :my_table, :serialized_column_raw, :text
    MyTable.update_all("serialized_column_raw = serialized_column")
    MyTable.update_all("serialized_column = NULL")
    MyTable.all.each do |mt|
      mt.serialized_column = OpenStruct.new(YAML::load(mt[:serialized_column_raw]))
      mt.save!
    end
    remove_column :my_table, :serialized_column_raw
</code>
