To change a single item option at runtime, call the [itemOption(id, option, value)](/api-reference/10%20UI%20Widgets/dxForm/3%20Methods/itemOption(id_option_value).md '/Documentation/ApiReference/UI_Widgets/dxForm/Methods/#itemOptionid_option_value') method.  This approach is more typical of jQuery. If the needed item is [in a group](/concepts/05%20Widgets/Form/10%20Organize%20Simple%20Items/05%20In%20Groups '/Documentation/Guide/Widgets/Form/Organize_Simple_Items/In_Groups/') or [in a tab](/concepts/05%20Widgets/Form/10%20Organize%20Simple%20Items/10%20In%20Tabs '/Documentation/Guide/Widgets/Form/Organize_Simple_Items/In_Tabs/'), the *field* parameter should be given the group caption or tab title followed by the item's name. An example is shown below.

    <!--JavaScript-->
    $(function() {
        var form = $("#formContainer").dxForm({
            formData: {
                firstName: "John",
                lastName: "Heart",
                phone: "+1(213) 555-9392",
                email: "jheart@dx-email.com"
            },
            items: ["firstName", "lastName", {
                itemType: "group",
                caption: "Contacts",
                items: ["phone", "email"]
            }]
        }).dxForm("instance");

        $("#checkBoxContainer").dxCheckBox({
            text: 'Show the Phone Number',
            value: true,
            onValueChanged: function (e) {
                form.itemOption("Contacts.phone", "visible", e.value);
            }
        });
    });

To change several options at a time, pass an object to the [itemOption(id, options)](/api-reference/10%20UI%20Widgets/dxForm/3%20Methods/itemOption(id_options).md '/Documentation/ApiReference/UI_Widgets/dxForm/Methods/#itemOptionid_options') method.
Being called with the *field* parameter only, this method returns the current configuration of the specified form item.

    <!--JavaScript-->
    $(function() {
        // ...
        $("#buttonContainer").dxButton({
            text: 'Change the Phone Options',
            onClick: function () {
                form.itemOption("Contacts.phone", {
                    isRequired: true, 
                    helpText: "+1(111)111-1111" 
                });
            }
        });
    });

With Angular, bind the option to change to a component or element property.
    
    <!--HTML-->
    <dx-form
        [(formData)]="employee">
        <dxi-item dataField="firstName"></dxi-item>
        <dxi-item dataField="lastName"></dxi-item>
        <dxi-item itemType="group" caption="Contacts">
            <dxi-item dataField="phone" [visible]="showPhone.value"></dxi-item>
            <dxi-item dataField="email"></dxi-item>
        </dxi-item>
    </dx-form>
    <dx-check-box #showPhone
        text="Show the Phone Number"
        [value]="true">
    </dx-check-box>

    <!--TypeScript-->
    import { DxFormModule, DxCheckBoxModule } from "devextreme-angular";
    // ...
    export class AppComponent {
        employee = {
            firstName: "John",
            lastName: "Heart",
            phone: "+1(213) 555-9392",
            email: "jheart@dx-email.com"
        }
    }
    @NgModule({
        imports: [
            // ...
            DxFormModule,
            DxCheckBoxModule
        ],
        // ...
    })

#####See Also#####
#include common-link-callmethods
- [Form - Change Editor Options at Runtime](/concepts/05%20Widgets/Form/20%20Change%20Options%20at%20Runtime/15%20Editor%20Options.md '/Documentation/Guide/Widgets/Form/Change_Options_at_Runtime/Editor_Options/')
- [Form - Configure Simple Items](/concepts/05%20Widgets/Form/05%20Configure%20Simple%20Items '/Documentation/Guide/Widgets/Form/Configure_Simple_Items/')
- [Form Demos](https://js.devexpress.com/Demos/WidgetsGallery/Demo/Form/GroupedFields)
- [Form API Reference](/api-reference/10%20UI%20Widgets/dxForm '/Documentation/ApiReference/UI_Widgets/dxForm/')

[tags]form, modify item, item option, change option
