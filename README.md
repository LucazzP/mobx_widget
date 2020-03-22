## ObserverFutureWidget - A simple Widget to handle MobX ObservableFuture events.


### Example usage

#### add dependency to pubspec.yaml
```dart
  mobx_widget:
    git: https://github.com/emanuel-braz/mobx_widget.git

 OR

  dependencies:
    mobx_widget: ^0.1.0
```

```dart
import 'package:mobx_widget/mobx_widget.dart';
```

#### Create the ObservableFuture
```dart
class MyStore {

  ...

  MyStore(){
    fetchData();
  }
  
  @observable
  ObservableFuture<String> myObservableFuture;
  
  @action
  Future<String> fetchData() async {
    return await (myObservableFuture = ObservableFuture( _repository.fetch() ));
  }
}
```

#### With Future (ObservableFuture)
```dart
...

ObserverFutureWidget(
  observableFuture: () => myStore.myObservableFuture,
  onResult: (_, data) => MyCustomDataWidget(data: data),
  onResultNull: (_) => Center(child: Text('Oops! No connection.')),
  onPending: (_) => CircularProgressIndicator(),
  onError: (_) => MyCustomErrorReloaderWidget(),
);
```

#### With Stream (ObservableStream)
```dart
...

ObserverStreamWidget(
  observableStream: () => myObservableStream,
  onData: (_, data) => Text('$data'),
  onNull: (_) => Text('NULL'),
  onUnstarted: (_) => Text('UNSTARTED'),
  onError: (_, error) => Text('ERROR: ' + error.toString())
)
```

### TODO
* add example
* add unit test
* add widget test
