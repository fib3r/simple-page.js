Simple-Page.js
==============

An ajax-based, Handlebars.js & Bootstrap powered data pager.

###Goal

Provide a simple way of paging client side data and utilize Handlebars.js 
as a template engine in presenting the data to the user. No need to specify
what fields are bounded to the control. Only you need to do a handlebars template, 
give it an ID, pass the ID in the initialization and you're golden.

### Example:

<script id="entry-template" type="text/x-handlebars-template">
    {% raw %}
    {{#if data}}
        
        {{#each data}}
        <div class="col-lg-3 col-md-3 col-sm-3 col-xs-4" style="margin-bottom: 30px;">
            <div class="thumbnail thumbnail-pinterest">
                <img src="{{ photo_url }}/{{ photo }}" style="width: 100%" />
                <div class="row no-margin">
                    <div class="col-sm-6">
                        <h3 class="pull-left">{{ sku }} - {{ id }}</h3>
                    </div>
                    <div class="col-sm-6">
                        <h3 class="pull-right">{{ price }} <small>Php</small></h3>
                    </div>
                </div>
                <div class="control-bar" style="background: #eee; border: 1px solid #e0e0e0; padding: 9px 10px;">
                <div class="row">
                    <div class="col-sm-6">
                        <div style="padding: 6px 0px 0px 6px;">
                            <strong class="label label-success">{{ item_count }}</strong> <small>In-Stock</small>
                        </div>
                    </div>
                    <div class="col-sm-6">
                        <div class="btn-group pull-right">
                            <a href="{% endraw %} {{ site_url('products/delete') }}{% raw %}/{{ id }}" class="btn btn-default btn-delete" title="Delete Product" data-title="{{ sku }}"><i class="icon-remove"></i></a>
                            <a href="{% endraw %}{{ site_url('products/update') }}{% raw %}/{{ id }}" class="btn btn-default" title="Edit Product" data-title="{{ sku }}"><i class="icon-pencil"></i> </a>
                        </div>
                    </div>
                </div>
                </div>
            </div>
        </div>
        {{/each}}
        
    {{else}}

        <div class="error-message" style="min-height: 380px;">
            <h1>You have no products or <br />your search request returned an empty result.</h1>
            <br />
            <p>
                You have not yet defined a product or set of products
                under your store.
            </p>
            <br />
            <br />
            <a href="{% endraw %}{{ site_url('products/create') }}{% raw %}" class="btn btn-default btn-lg btn-primary">Add Product</a>
            <a href="{% endraw %}{{ site_url('products') }}{% raw %}" class="btn btn-default btn-lg">Products Home</a>
        </div>

    {{/if}}
    {% endraw %}
</script>   

<div id="products-container"></div>


    <script type="text/javascript" src="path-to/simple-page.js"></script>

    <script type="text/javascript">
        $(document).ready(function() {

            $('#products-container').simplePage({
                source       :  'path-to/json.php',
                template     :  '#entry-template',
                sort_fields  :  {
                                    'sku': 'SKU',
                                    'price': 'Price',
                                    'description': 'Description'
                                },
                per_page     :  5,
                pager_top    :  true,
                pager_bottom :  true,
                preloader    :  false,
                callback     :  function(e) {

                    // 

                }
            });

        });

    </script>
