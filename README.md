
![](logo.png)

## Quickstart for testing with Electron
This is a basic Electron testing setup. It combines Spectron and the test-runner Ava. This allows you to quickly start an Electron project with a testing pipeline already active. 

Electron Version: **5.0.0**

Spectron Version: **7.0.0**

### Setup

``` bash
npm install
```

For **Testing**:

``` bash
npm test
```

For **Starting**:

``` bash
npm start
```

### A bit more in-depth
First of all it's important to start and close **Electron** before and after all tests. We do this like this in the `test.js` file:

``` javascript
//Application gets started before testing
test.before(t => {
    app = new Application({
        path: electronPath,
        args: ['main.js'],
        startTimeout: timeout,
        waitTimeout: timeout,
    })

    return app.start()
});

//And closed after testing
test.after(t => {
    if (app && app.isRunning()) {
        return app.stop()
    }
});
```
This functionality is enabled by **Spectron**. The test themselves are written with the syntax defined by **Ava**.

``` javascript
test('Window was launched', async t => {
    t.is(await app.client.getWindowCount(), 1)
});

test('HTML was loaded', async t => {
    t.is(await app.client.getTitle(), 'Title of my HTML-file')
});
```

Here the async-enabled syntax of **Ava** really shines. 

### About
Made by Sebastian Schuchmann. Free for commerical and personal use. 

Enjoy!

