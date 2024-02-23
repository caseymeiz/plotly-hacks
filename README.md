## Print camera position in HTML viewer

paste into js console

```js
plotElement = document.querySelector('.plotly-graph-div');
if (plotElement) {
    plotElement.on('plotly_relayout', function(eventData) {
        const sceneRegex = /scene(\d*)\.camera/;
        Object.keys(eventData).forEach(key => {
            const match = key.match(sceneRegex);
            if (match) {
                const camera = eventData[key];
                const sceneNumber = match[1];
                const sceneName = sceneNumber ? `scene${sceneNumber}` : 'scene';
                const formattedOutput = `${sceneName}_camera=dict(\n` +
                    `    eye=dict(x=${camera.eye.x}, y=${camera.eye.y}, z=${camera.eye.z}),\n` +
                    `    up=dict(x=${camera.up.x}, y=${camera.up.y}, z=${camera.up.z}),\n` +
                    `    center=dict(x=${camera.center.x}, y=${camera.center.y}, z=${camera.center.z}),\n` +
                    `)`;
                console.log(formattedOutput);
            }
        });
    });
} else {
    console.log('Plotly plot not found. Ensure you are running this in the console of a page with a Plotly 3D plot.');
}
```

