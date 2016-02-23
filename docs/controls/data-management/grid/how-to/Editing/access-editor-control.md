---
title: Access Editor Controls in Edit Events
page_title:  Access Editor Controls in Edit Events | Kendo UI Grid
description: "Learn how to access an editor control in the edit event handler of the Kendo UI Grid widget."
slug: howto_access_editor_controlsin_edit_events_grid
---

# Access Editor Controls in Edit Events

The example below demonstrates how to acccess an editor control in the `edit` event handler of the Kendo UI Grid widget.

###### Example

```html
<script src="http://demos.telerik.com/kendo-ui/content/shared/js/products.js"></script>
<div id="example">
    <div id="grid"></div>

    <script>

        $(document).ready(function () {
            var dataSource = new kendo.data.DataSource({
               pageSize: 20,
               data: products,
               autoSync: true,
               schema: {
                   model: {
                     id: "ProductID",
                     fields: {
                        ProductID: { editable: false, nullable: true },
                        ProductName: { validation: { required: true } },
                        Category: { defaultValue: { CategoryID: 1, CategoryName: "Beverages"} },
                        UnitPrice: { type: "number", validation: { required: true, min: 1} }
                     }
                   }
               }
            });

            $("#grid").kendoGrid({
                dataSource: dataSource,
                pageable: true,
                height: 550,
                toolbar: ["create"],
                columns: [
                    { field:"ProductName",title:"Product Name" },
                    { field: "Category", title: "Category", width: "180px", editor: categoryDropDownEditor, template: "#=Category.CategoryName#" },
                    { field: "UnitPrice", title:"Unit Price", format: "{0:c}", width: "130px" },
                    { command: "edit", title: " ", width: "150px" }],
                editable: "inline",
                edit: function(e) {
                  var model = e.model; //reference to the model that is about the be edited

                  var container = e.container; //reference to the editor container

                  var category = container.find("[data-role=dropdownlist]").data("kendoDropDownList"); //find widget element

                  //if widget is found (required for incell editing)
                  if (category) {
                    //use DropDownList API based on the model values to accomplish your bussiness requirement.

                    //link: http://docs.telerik.com/kendo-ui/api/javascript/ui/dropdownlist
                  }
                }
            });
        });

        function categoryDropDownEditor(container, options) {
            $('<input required data-text-field="CategoryName" data-value-field="CategoryID" data-bind="value:' + options.field + '"/>')
                .appendTo(container)
                .kendoDropDownList({
                    autoBind: false,
                    dataSource: {
                        type: "odata",
                        transport: {
                            read: "http://demos.telerik.com/kendo-ui/service/Northwind.svc/Categories"
                        }
                    }
                });
        }

    </script>
</div>
```

## See Also

Other articles on Kendo UI Grid and how-to examples related to its editing functionality:

* [JavaScript API Reference](/api/javascript/ui/grid)
* [How to Add New Rows When Tabbing out of the Last One]({% slug howto_add_new_rows_when_tabbingoutof_thelast_one_grid %})
* [How to Build Custom dataSource for Custom Editor]({% slug howto_build_custom_datasourcefor_custom_editor_grid %})
* [How to Customize the Delete Confirmation Dialog]({% slug howto_customize_delete_confirmation_dialog_grid %})
* [How to Delete Multiple Rows Selected with Checkboxes]({% slug howto_delete_rows_selectedwith_checkboxes_grid %})
* [How to Edit Records in Child Grids]({% slug howto_edit_recordsin_children_grid %})
* [How to Edit Records Using External Forms]({% slug howto_edit_records_using_external_forms_grid %})
* [How to Increase Popup Edit Form and Textbox Width]({% slug howto_increase_popup_edit_formand_textbox_grid %})
* [How to Preserve Dirty Indicator in Incell Editing and Client Operations]({% slug howto_preserve_dirty_indicator_incell_editing_client_operations_grid %})
* [How to Prevent Editing for Boolean Based Records]({% slug howto_prevent_editingfor_boolean_based_records_grid %})
* [How to Prevent Page Navigation in Edit Mode]({% slug howto_prevent_page_navigation_inedit_mode_grid %})
* [How to Render Grid Editor in Column Template]({% slug howto_render_editor_column_template_grid %})
* [How to Show Custom Editor Using the Selected Item outside the Grid]({% slug howto_use_show_custom_editor_selected_item_outside_grid %})
* [How to Show Edit Buttons for Editable Records Only]({% slug howto_show_editfor_editable_records_only_grid %})
* [How to Use AutoComplete as Custom Column Editor]({% slug howto_use_autocompleteas_custom_column_editor_grid %})
* [How to Use ASMX Service with CRUD Operations]({% slug howto_crud_web_service_grid %})
* [How to Use WCF with CRUD Operations]({% slug howto_use_wcf_service_crud_operations_grid %})
* [How to Use CRUD Operations When Grid Is Bound through MVVM]({% slug howto_use_crud_operationswith_mvvmbound_grid %})
* [How to Use CRUD Operations When Grid Is Bound to ASP.NET MVC Action Methods]({% slug howto_use_crud_operationswith_apsnet_action_methods_bound_grid %})
* [How to Use CRUD Operations when Grid Is Bound to Web Methods]({% slug howto_use_crud_boundto_web_methods_grid %})
* [How to Use Editors Based on Data Item Property]({% slug howto_use_editors_basedon_dataitem_property_grid %})
* [How to Use MultiSelect as CSV Editor]({% slug howto_usethe_multiselect_aseditor_commaseparated_stringfields_grid %})
* [How to Use TreeView as Custom Editor]({% slug howto_usethe_treeview_aseditor_grid %})
