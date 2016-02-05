# kibana-executor-service
A periodical executor service for Kibana

## Requirements
- Kibana 4.4+

## Example Usage

```javascript
import modules from 'ui/modules';
import 'kibana-executor-service';
var app = modules.get('app/example', ['kibana/executor']);

app.controller('exampleController', function ($executor, timefilter, $scope, $http) {
  timefilter.enabled = true;
  
  $executor.register({
    execute: () => {
      // Do some periodic task like hit an HTTP api endpoint
      $http.get('/something/very/cool');
    },
    handleResponse: (resp) => {
      // Sweet dude!
    },
    handleError: (err) => {
      // Oops!
    }
  });

  // Start the executor
  $executor.start();

  // Destory the executor
  $scope.$on('$destroy', $executor.destroy);

});
```
