---
layout: page
title: Documentation
permalink: /doc/
---

# Nested form fields validation (cross component)

# Vanilla JS clipboard copy / paste

# On initialize expression

# Bootstrap

## Popup

### Overview

{% highlight ts %}
class Modal {
    create ({
        component, providers = [],
        modalParentSelector = "[a2modalHolder]",
        keyboard = true,
        show = true,
        backdrop = true
    }: ModalOptions): Observable<ModalInstance> {}
}

interface ModalOptions {
    component: ng.Type|string;
    providers?: Array<ng.Type | any[] | any>;
    modalParentSelector?: string;
    backdrop?: ModalBackdrop;
    show?: boolean;
    keyboard?: boolean;
}

type ModalBackdrop = "static" | boolean;

interface ModalInstance {
    jqueryElement: any;
    result: Observable<any>;
    discard (): void;
    close (val: any): void;
    error (val: any): void;
}

class ModalActions {
    discard (): void {}
    close (val: any): void {}
    error (val: any): void {}
}

{% endhighlight %}

### Description
Displays modal window.

#### ModalOptions

`component: ng.Type|string`
Popup component type.

{% highlight ts %}
import * as ng from "@angular/core";
import {ModalActions} from "../bootstrap/modal/modal";

export const MY_MODAL_DEPENDENCY: ng.OpaqueToken =
    new ng.OpaqueToken("myModalDependency");

@ng.Component({
    selector: "my-modal",
    templateUrl: "src/examples/MyModal.component.html"
})
export class MyModalComponent {
    constructor (@ng.Inject(MY_MODAL_DEPENDENCY) public dynamicDependency: any,
                 public actions: ModalActions) {}
    discard (): void { this.actions.discard(); }
    close (): void { this.actions.close({"my": "data to return from popup"}); }
    error (): void { this.actions.error({"close": "with error data"}); }
}

{% endhighlight %}


`providers?: Array<ng.Type | any[] | any>`

Custom dependencies.

Default: Inherits component injector with `ModalActions`.

{% highlight ts %}
modal.create({
        component: MyModalComponent,
        providers: [{provide: MY_MODAL_DEPENDENCY, useValue: 42}]
    })
{% endhighlight %}


`modalParentSelector?: string`

There have to be element in DOM that can be found by modalParentSelector.

{% highlight html %}
<body>
<!-- ... -->
<div a2modalHolder> <!-- It is necessary -->
    <!-- Here will be added content of modal window -->
</div>
<!-- ... -->
</body>
{% endhighlight %}

`backdrop?: ModalBackdrop` Dark overlay behind modal.
[Bootstrap Docs](http://getbootstrap.com/javascript/#modals-options)

`show?: boolean` Show modal when initialized.
[Bootstrap Docs](http://getbootstrap.com/javascript/#modals-options)

`keyboard?: boolean` Modal can be closed by Esc button.
[Bootstrap Docs](http://getbootstrap.com/javascript/#modals-options)

#### ModalInstance
Created modal instance

`jqueryElement: any` JQuery element created by $(myElement).modal(...).

`result: Observable<any>` Result data from modal.

`discard (): void` Closes modal without success/error result.

`close (val: any): void` Closes modal with success result.

`error (val: any): void` Closes modal with error result.
