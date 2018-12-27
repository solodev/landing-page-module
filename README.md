# landing-page-module

## Prerequisites
<ul>
	<li><a target="_blank" href="https://getbootstrap.com/">Boostrap4</a></li>
	<li><a target="_blank" href="https://fontawesome.com/">FontAwesome5</a></li>
</ul>

## Step 1: Add the Form
 - landing-page-form.tpl

Create a calendar for the Landing Page and upload the following form. Be sure to replace SITE_NAME with your site's name.

```
<div class="panel-group">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h4 class="panel-title">
                <a data-toggle="collapse" href="#collapseStatus" aria-expanded="true">Post Status<span class="toggle"aria-hidden="true"></span></a>
            </h4>
        </div>
        <div id="collapseStatus" class="panel-collapse collapse in">
            <div class="panel-body">
                <div class="row">
                    <div class="col-md-3">
                        <h2><label class="label-control" for="post_status">Post Status</label></h2>
                        <select class="form-control" type="text" name="post_status">
                            <option value="Draft">Draft</option>
                            <option value="Published">Published</option>
                        </select>
                    </div>
                   
                </div>
            </div>
        </div>
    </div>
</div>


<div class="panel-group">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h4 class="panel-title">
                <a data-toggle="collapse" href="#collapseResourceContent" aria-expanded="true">FAQs <span class="toggle" aria-hidden="true"></span></a>
            </h4>
        </div>
        <div id="collapseResourceContent" class="panel-collapse collapse in">
            <div class="panel-body">
                <div class="row">
                    <div class="col-md-12">
                        <h2><label class="label-control" for="heading_title">FAQ Question</label></h2>
                        <p class="subText">(Required)</p>
                        <input type="text" class="form-control" name="heading_title" id="heading_title">
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-12">
                        <h2><label class="label-control" for="faq_answer">FAQ Answer</label></h2>
                        <p class="subText">(Required)</p>
                        <textarea class="form-control wysiwyg2" name="faq_answer" id="faq_answer"></textarea>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<div class="panel-group">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h4 class="panel-title">
                <a data-toggle="collapse" href="#collapseMeta">META Data <span class="toggle" aria-hidden="true"></span></a>
            </h4>
        </div>
        <div id="collapseMeta" class="panel-collapse collapse">
            <div class="panel-body">
                <div class="row">
                    <div class="col-md-12">
                        <h2><label name="meta_title">Meta Title</label></h2>
                        <p class="subText">(Optional) Include a custom META Title that will show in your browser tab and in the page's source code.</p>
                        <input type="text" class="form-control" name="meta_title" id="meta_title">
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-12">
                        <h2><label name="meta_description">Meta Description</label></h2>
                        <p class="subText">(Optional) Include a custom META Description that search engines will index. 50-160 Characters</p>
                        <textarea class="form-control" id="meta_description" name="meta_description"></textarea>
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-12">
                        <h2><label name="meta_keywords">Meta Keywords</label></h2>
                        <p class="subText">(Optional) Include the main keywords of the blog article.</p>
                        <textarea class="form-control" id="meta_keywords" name="meta_keywords"></textarea>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<div class="panel-group">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h4 class="panel-title">
                <a data-toggle="collapse" href="#collapseAdvanced">Advanced <span class="toggle" aria-hidden="true"></span></a>
            </h4>
        </div>
        <div id="collapseAdvanced" class="panel-collapse collapse">
            <div class="panel-body">
                <div class="row">
                    <div class="col-md-12">
                        <h2><label class="label-control" for="post_javascript">Custom JavaScript</label></h2>
                        <p class="subText">(Optional) Use the following textbox to embed any custom JavaScript including tracking pixels and Google Analytics scripts. Be sure to open your JavaScript with a &lt;script&gt; tag and close everything with a &lt;/script&gt; tag.</p>
                        <textarea class="form-control" name="post_javascript" id="post_javascript"></textarea>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<?php
      if(isset($dataVars['calendar_entry_id'])){     
        $calendar_entry = new Calendar_Entry($dataVars['calendar_entry_id']);
        if($calendar_entry->path) { 
    ?>
<div class="panel-group">
    <div class="panel panel-default">
        <div class="panel-heading">
            <h4 class="panel-title">
                <a data-toggle="collapse" href="#collapseURL">Post URL <span class="toggle" aria-hidden="true"></span></a>
            </h4>
        </div>
        <div id="collapseURL" class="panel-collapse collapse in">
            <div class="panel-body">
                <div class="row">
                    <div class="col-md-12">
                        <p class="subText">You can access this blog post at the following URL:</p>
                        <a href="https://www.SITE_NAME.com<?= $calendar_entry->path ?>" target="_blank">https://www.SITE_NAME.com<?= $calendar_entry->path ?></a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<?php 
        } 
      }
     ?>

<script>
    $('.wysiwyg').ckeditor(function () {}, {
        customConfig: '/CK/config.js',
        height: '600px',
        basePath: '/CK/',
        toolbar: 'WP'
    });
</script>

```

## Step 2: Add the detail template
 - landing-page-detail.tpl

Add the following detail template. 

```
[entry]
	  <section class="container my-5">
      <div class="row">
        <div class="col-lg-7 col-xl-8 pr-lg-5">
           [is_empty value="{{heading_title}}"]
           	<h1 class="h2 mt-4 mb-0"><strong>{{event_title}}</strong></h1>
           [/is_empty]
           <img src="[get_asset_file_url id={{main_image}}]" class="img-fluid my-5" alt="{{event_title}} Feature Image">
           {{landing_page_content}}
        </div>

        <aside class="col-lg-5 col-xl-4">
          <form action="{{formcall}}" method="post" role="form" data-toggle="validator">
               <div class="primary-top-border bg-light-gray mt-sm-4 mt-md-0 p-5">
                  <h3 class="text-uppercase mb-5 text-center"><strong>{{formtitle}}</strong></h3>
                  <div class="form-group mt-4">
                    <label class="font-weight-bold" for="prospect_fname">First Name <span class="text-scarlet">*</span></label> 
                    <input type="text" name="prospect_fname" id="prospect_fname" class="form-control rounded-0 required w-100">
                  </div>
                  <div class="form-group mt-4">
                    <label class="font-weight-bold" for="prospect_lname">Last Name <span class="text-scarlet">*</span></label> 
                    <input type="text" name="prospect_lname" id="prospect_lname" class="form-control rounded-0 required w-100">
                  </div>
                  <div class="form-group">
                    <label class="font-weight-bold" for="email">Email <span class="text-scarlet">*</span></label> 
                    <input type="text" name="email" id="email" class="form-control rounded-0 required w-100">
                  </div>
                  <div class="form-group mt-3">
                    <label class="font-weight-bold" for="title">Title</label> 
                    <input type="text" name="title" id="title" class="form-control rounded-0 w-100">
                  </div>
                  <div class="form-group mt-3">
                    <label class="font-weight-bold" for="company">Company</label> 
                    <input type="text" name="company" id="company" class="form-control rounded-0 w-100">
                  </div>
                  <div class="form-group mt-3">
                    <label class="font-weight-bold" for="phone">Phone</label> 
                    <input type="text" name="phone" id="phone" class="form-control rounded-0 w-100 mt-1">
                  </div>
                  <div class="text-center">
                    <input type="submit" class="btn btn-primary btn-lg mt-3" value="{{formtext}}">
                  </div>
                </div>
             </form>
        </aside>
      </div>
    </section>
    <section class="bg-primary-dark text-center text-white py-5 mt-sm-5">
      <div class="container">
        <div class="w-lg-50 w-md-75 mx-auto">
          <h2>{{mid_title}}</h2>
          <p>{{mid_content_supporting}}</p>
        </div>
        <!-- Begin Fourbox -->

    <div class="row mt-lg-5">
      <div class="col-md-6 col-lg-3 mt-sm-4">
        <i class="fa-2x {{box_1_icon}}"></i>
        <h3 class="h4 text-uppercase mt-3">{{box_1_heading}}</h3>
        <p>{{box_1_text}}</p>
      </div>
      <div class="col-md-6 col-lg-3 mt-sm-4">
        <i class="fa-2x {{box_2_icon}}"></i>
        <h3 class="h4 text-uppercase mt-3">{{box_2_heading}}</h3>
        <p>{{box_2_text}}</p>
      </div>
      <div class="col-md-6 col-lg-3 mt-sm-4">
        <i class="fa-2x {{box_3_icon}}"></i>
        <h3 class="h4 text-uppercase mt-3">{{box_3_heading}}</h3>
        <p>{{box_3_text}}</p>
      </div>
      <div class="col-md-6 col-lg-3 mt-sm-4">
        <i class="fa-2x {{box_4_icon}}"></i>
        <h3 class="h4 text-uppercase mt-3">{{box_4_heading}}</h3>
        <p>{{box_4_text}}</p>
      </div>
    </div>
        [cond type="is" subject="{{linktype}}" value="Internal"]
        	<a href="{{internal_page}}" class="btn btn-secondary btn-lg mt-md-5 mt-sm-4">{{mid_content_btn}}</a>
        [/cond]
        [cond type="is" subject="{{linktype}}" value="External"]
        	<a href="{{external_page}}" class="btn btn-secondary btn-lg mt-md-5 mt-sm-4">{{mid_content_btn}}</a>
        [/cond]
      </div>
    </section>
    <section class="bg-light-gray">
      <div class="container">
        <div class="row">
          <div class="col-md-5 py-3"><img alt="{{bottom_tile_title}} Image" class="img-fluid" src="[get_asset_file_url id={{bottom_tile_image}}]"></div>
          <div class="col-md-6 py-3 ml-auto d-flex align-items-center">
            <div>
              <h3>{{bottom_tile_title}}</h3>
              <p>{{bottom_tile_text}}</p>
              <a class="btn btn-lg btn-primary" href="{{bottom_cta_link}}">{{bottom_cta_text}}</a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <div class="bg-secondary text-white py-4 small">
     <div class="container">
      <div class="row align-items-center justify-content-between">
        <div class="col-sm-6 text-center text-lg-left col-lg-3"><a href="/"><img alt="Logo" class="w-75" src="/_/images/logo.png" /></a></div>

        <div class="col-sm-6 text-center col-lg-3">
          <p class="m-0">© 2018 WebCorpCo. All Rights Reserved.</p>
        </div>

        <div class="col-sm-6 text-center col-lg-3">
          <ul class="list-unstyled list-inline list-bordered mb-0">
            <li class="list-inline-item"><a class="text-white" href="/sitemap.stml">Site Map</a></li>
            <li class="list-inline-item"><a class="text-white" href="/privacy-policy.stml">Privacy Policy</a></li>
            <li class="list-inline-item"><a class="text-white" href="/contact-us.stml">Contact Us</a></li>
          </ul>
        </div>

        <div class="col-sm-6 text-center text-lg-right col-lg-3">
          <p class="m-0">Powered by <a class="text-light" href="https://www.solodev.com" target="_blank">Solodev CMS</a></p>
        </div>
      </div>
    </div>
  </div>
  {{post_javascript}}
[/entry]


```


## Step 5: Add the SCSS/CSS
 - /_/scss/landing-page.scss
 
 ```
 
 .primary-top-border {
    border-top: solid 6px #d60e96;
}
.small, small {
    font-size: 88%;
}

 ```
