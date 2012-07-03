#Event Handling

An event is a way a view to notify some interesting thing happens to the view.
For example, the `click` event notifies the user touches it, and the `layout` event notifies the view has been positioned by the layout manger.

##Listen to Events

You can use the `on` method to listen the events of a view:

    button.on.click.add((event) {
      doSomething(event.target);
    });

As shown, the argument is an event listener. An event listener is a closure that takes an instance of [ViewEvent](http://rikulo.org/api/_/event/ViewEvent.html) or its derives as the argument.

The class of an event depends on the event itself. For example, the `change` event is sent with an instance of [ChangeEvent](http://rikulo.org/api/_/event/ChangeEvent.html). For example,

    TextBox textBox = new TextBox();
    textBox.on.change((ChangeEvent event) {
      print("${event.value}");
    });

##Send and Post Events

Events are usually sent by a view. However, the application can send the application-specific events too.

    view.sendEvent(new ViewEvent("foo"));

On the other hand, you can listen to the application-specific event as follows.

    view.on['foo'].add(fooListener);

> Notice that `on.click` is equivalent to `on['click']`. It is one of built-in properties provided by [ViewEvents](http://rikulo.org/api/_/event/ViewEvents.html) (which is the class of the object returned by the `on` method).

The `sendEvent` method will invoke all registered event listeners before returning. If you prefer to queue the event and invoke the event listeners later, you can use `postEvent` instead.

##Broadcast Events