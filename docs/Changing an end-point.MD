# Changing an end-point

In this example, we change `grant` to `grant_write_permission_to_stream`

## 1. Change the following in routes.js:
```
var grant = require('./functions/grant');
to
var grant_write_permission_to_stream = require('./functions/grant_write_permission_to_stream');
```
```
router.post('/api/v1/grant', (req, res) => {
to
router.post('/api/v1/grant_write_permission_to_stream', (req, res) => {
```
```
grant.grant(address, stream_name)
to
grant_write_permission_to_stream.grant_write_permission_to_stream(address, stream_name)
```

## 2. Change the following in functions/grant.js
```
exports.grant = (address, stream_name) => {
to
exports.grant_write_permission_to_stream = (address, stream_name) => {
```

## 3. Rename functions/grant.js
```
functions/grant.js
to
functions/grant_write_permission_to_stream.js
```

