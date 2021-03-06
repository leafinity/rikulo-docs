#Advanced Topics

##[View.isViewGroup](api:view)

[View.isViewGroup](api:view) indicates whether the given view is a view group.
A view group can contains other views (called child views). If false, an exception is thrown when [View.addChild()](api:view) is called.


##[View.addChildNode_()](api:view)

When [View.addChild()](api:view) is called, [View](api:view) will invoke
[View.addChildNode_()](api:view) at the end to add the DOM element of the child view into the DOM tree.

By default, the child element will be added right under `node`. In other words, it assumes the view has only one layer of DOM elements. If you'd like to put the child elements in a particular location, you have to override this method.

For example, assume the child element to put the child elements is identified as `cnt`, then you can do as follows

    void addChildNode_(View child, View beforeChild) {
      if (beforeChild !== null)
        super.addChildNode_(child, beforeChild);
      else
        getNode('cnt').nodes.add(child.node);
    }

#[View.mount_()](api:view) and [View.unmount_()](api:view)

When a hierarchy of views are added to the browser (i.e., [View.addToDocument()](api:view) is called), [View.mount_()](api:view) will be called for every view in the hierarchy.

Similarly, [View.unmount_()](api:view) will be called if it is detached (i.e., [View.remove()](api:view)).

For example, if you want [Layout Manager](../../Layouts/LayoutManager.md) to defer until a particular image is loaded, you can do as follows.

    void mount_() {
      super.mount_(); //call back super first
      layoutManager.waitImageLoaded("foo.png");
    }

> [LayoutManager.waitImageLoaded()](api:layout) is a utility to have the layout manager wait for particular image to load before handling the layout of views.
