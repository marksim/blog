---
layout: post
title: PDF Generation in Rails... The Right Way
categories: blog
---
As long as we're talking about efficiency here, one of the ways to be more efficient is to use the right tool for the job.  I've done PDF generation on 3 different projects but the PDF generation I did yesterday was by far the easiest.   What I thought would take me 2 days ended up taking about 3 hours (with research, etc).

If you're not using Ruby to automate some part of your job or life, I feel sad for you (at least a little).   The next time you need to generate PDFs, why not try out the excellent <a title="Prawn : PDF Generation Done Right" href="http://github.com/sandal/prawn" target="_blank">Prawn</a> library?  Not familiar, you say?   Well, let's dive right in, shall we?

For those of you that used Prawn in an earlier 0.3 form, it's recently been drastically improved and released as 0.7 in a push towards 1.0.  The APIs are very full featured (if sometimes a wee bit clunky--but PDF generation is a messy business) and simple to use.  All of this is even better when integrating Prawn into Rails as a template builder using prawnto:

<code lang="bash">
./script/plugin install git://github.com/huerlisi/prawnto.git
</code>

Even though thorny-sun originally wrote prawnto, their branch is no longer maintained, it appears.  Thank goodness for github since huerlisi seems to have picked up right where they left off.

Once we've got prawnto installed, there isn't actually anything else we need to do to be ready to generate PDFs in our views.   Let's start of with something useful.   A table in show.pdf.prawn:

<code lang="ruby">
pdf.font 'Courier' do
  pdf.table object.line_items.collect {|li| 
  		[ 
  			li.description, 
  			(li.quantity.nil? ? "" : "#{li.quantity}"), 
  			(li.rate.to_f == 0 ? "" : number_to_currency(li.rate)), 
  			(li.amount.to_f == 0 ? "" : number_to_currency(li.amount))
  		]
  	}, 
  	:font_size => 8,
  	:vertical_padding => 2,
  	:headers => ["Description", "Quantity", "Rate", "Amount"],
  	:header_color => "888888",
  	:header_text_color => "FFFFFF",
  	:border_width => 1,
  	:width => pdf.bounds.width,
  	:column_widths => {0 => pdf.bounds.width-180},
  	:align => {2 => :right, 3 => :right}
end
</code>

Tell me that isn't readable?   30 seconds and you can tell exactly what that's doing.

And we can even extract it to a partial!   The only thing you have to do to make it a partial is rename the pdf object to something else, conventionally "parent_pdf"

<code lang="ruby">
parent_pdf.font 'Courier' do
  parent_pdf.table object.line_items.collect {|li| 
  		[ 
  			li.description, 
  			(li.quantity.nil? ? "" : "#{li.quantity}"), 
       ...
    # etc...
</code>

And then call the partial from show.pdf.prawn

<code lang="ruby">
render :partial => 'object', :locals => {:object => @object, :parent_pdf => pdf}
</code>

and index.pdf.prawn

<code lang="ruby">
first = true
@objects.each do |object|
  pdf.start_new_page unless first
  render :partial => 'object', :locals => {:object => object, :parent_pdf => pdf}
  first = false
end
</code>

And make sure our controller actions can respond to the '.pdf' format.

<code lang="ruby">
  def show
    @object = Object.find(params[:id])
    respond_to do |format| 
      format.pdf do
        send_data(render(:template => 'objects/show.pdf.prawn', :layout => false), 
          :filename => "#{object.name}.pdf", 
          :type => 'application/pdf', 
          :disposition => 'attachment')
      end
    end
  end

  def index
    @objects = Object.all
    respond_to do |format| 
      format.pdf do
        send_data(render(:template => 'objects/index.pdf.prawn', :layout => false), 
          :filename => "objects.pdf", 
          :type => 'application/pdf', 
          :disposition => 'attachment')
      end
    end
  end
</code>

Everything is separated where it needs to be.  All the view logic is in the views, model logic is in the models, and controller logic isn't duplicated elsewhere.  

Make sure and check out the <a href="http://github.com/sandal/prawn/tree/master/examples/">various</a> <a href="http://github.com/sandal/prawn-layout/tree/master/examples/">Prawn</a> <a href="http://github.com/madriska/prawn-security/tree/stable/examples">examples</a> and do your next PDF generation right.
