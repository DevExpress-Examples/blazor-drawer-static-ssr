<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/848649591/24.1.3%2B)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T1250630)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
[![](https://img.shields.io/badge/💬_Leave_Feedback-feecdd?style=flat-square)](#does-this-example-address-your-development-requirementsobjectives)
<!-- default badges end -->
# Drawer for Blazor - Responsive Drawer in Static SSR Mode

This example implements a responsive drawer when using static SSR mode.

The [DevExpress Blazor Drawer](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxDrawer) component requires interactive render mode to change its [IsOpen](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxDrawer.IsOpen) state. Use one of the following strategies to dynamically change drawer visibility in static SSR mode.

* Add query params to control drawer visibility. This approach is used within DevExpress Blazor [project templates](https://docs.devexpress.com/Blazor/401057/get-started?v=24.2#devexpress-project-templates) (v24.1.6+). 
* Specify CSS rules to control drawer visibility (this example).
  
![Responsive Drawer](drawer.gif)

## Implementation Details

This example contains two nested instances of the DevExpress Blazor Drawe (DxDrawer) component. The first (external) drawer is configured for use on desktop devices - the second (internal) drawer is configured for use on mobile devices (less than 769px).

```html
<DxDrawer PanelWidth="240px" CssClass="navigation-drawer" Mode="@DrawerMode.Shrink" IsOpen="@true" >
    <BodyTemplate>
        @DrawerBody
    </BodyTemplate>
    <TargetContent>
        <DxDrawer PanelWidth="240px" CssClass="navigation-drawer mobile" Mode="@DrawerMode.Overlap" IsOpen="@true">
            <BodyTemplate>
                @DrawerBody
            </BodyTemplate>
            <TargetContent>
                @DrawerTarget
            </TargetContent>
        </DxDrawer>
    </TargetContent>
</DxDrawer>
```

Users can click a checkbox element to open or close the drawer.

```html
<input type="checkbox" title="Toggle Nav" class="navbar-toggler icon icon-menu menu-button" checked />
```

The CSS file ([MainLayout.razor.css](./CS/DxDrawerExample/Components/Layout/MainLayout.razor.css)) specifies rules to open or close the drawer based on viewport size and checkbox state.

```css
/* Display the first drawer (for desktop) */
::deep .navigation-drawer > .dxbl-drawer-panel {
    display: flex;
}
/* Collapse or expand the first drawer based on the toggle button state */
::deep.page:has(.navbar-toggler:not(:checked)) .navigation-drawer:not(.mobile) > .dxbl-drawer-panel {
    width: 0 !important;
}
/* Hide the second drawer (for mobile) */
::deep .navigation-drawer.mobile > .dxbl-drawer-panel {
    display: none;
}

@media (max-width: 768px) {
    /* Hide the first drawer (for desktop) */
    ::deep .navigation-drawer > .dxbl-drawer-panel {
        display: none;
    }
    /* Display the second drawer (for mobile) */
    ::deep .navigation-drawer.mobile > .dxbl-drawer-panel {
        display: flex;
    }
    /* Collapse or expand the second drawer based on the toggle button state */
    ::deep.page:has(.navbar-toggler:checked) .navigation-drawer.mobile > .dxbl-drawer-panel {
        width: 0 !important;
    }
}
```

## Files to Review

* [MainLayout.razor](./CS/DxDrawerExample/Components/Layout/MainLayout.razor)
* [NavMenu.razor](./CS/DxDrawerExample/Components/Layout/NavMenu.razor)
* [Drawer.razor](./CS/DxDrawerExample/Components/Layout/Drawer.razor)
* [MainLayout.razor.css](./CS/DxDrawerExample/Components/Layout/MainLayout.razor.css)

## Documentation

- [DxDrawer class](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxDrawer)

<!-- feedback -->
## Does this example address your development requirements/objectives?

[<img src="https://www.devexpress.com/support/examples/i/yes-button.svg"/>](https://www.devexpress.com/support/examples/survey.xml?utm_source=github&utm_campaign=blazor-drawer-static-ssr&~~~was_helpful=yes) [<img src="https://www.devexpress.com/support/examples/i/no-button.svg"/>](https://www.devexpress.com/support/examples/survey.xml?utm_source=github&utm_campaign=blazor-drawer-static-ssr&~~~was_helpful=no)

(you will be redirected to DevExpress.com to submit your response)
<!-- feedback end -->
