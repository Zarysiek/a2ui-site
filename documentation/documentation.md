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

interface ModalInstance {
    jqueryElement: any;
    result: Observable<any>;
    discard (): void;
    close (val: any): void;
    error (val: any): void;
}

{% endhighlight %}

### Description

### Example



<div style="color: red;">Asd</div>