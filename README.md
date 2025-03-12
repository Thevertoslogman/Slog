// ==UserScript==

// @name         Weap3
// @namespace    http://tampermonkey.net/
// @version      v3.0
// @description  Weap loader
// @author       Weapon
// @include      https://pixelplace.io/*
// @icon         https://uploads.scratch.mit.edu/get_image/user/51380016_60x60.png
// @require      https://pixelplace.io/js/jquery.min.js?v2=1
// @require      https://pixelplace.io/js/jquery-ui.min.js?v2=1
// @require      https://cdnjs.cloudflare.com/ajax/libs/toastr.js/2.1.4/toastr.min.js
// @run-at       document-start
// @grant        none
// ==/UserScript==

//Sorry i had to use @include!
//I thought it would be better
globalThis['5d69f6dbccb2c45145f48adfbfce81b3'] = new Object();
(function() {const palette = {
    order: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48],
    colors: ['#FFFFFF', '#C4C4C4', '#888888', '#555555', '#222222', '#000000', '#006600', '#22B14C', '#02BE01', '#51E119', '#94E044', '#FBFF5B', '#E5D900', '#E6BE0C', '#E59500', '#A06A42', '#99530D', '#633C1F', '#6B0000', '#9F0000', '#E50000', '#FF3904', '#BB4F00', '#FF755F', '#FFC49F', '#FFDFCC', '#FFA7D1', '#CF6EE4', '#EC08EC', '#820080', '#5100FF', '#020763', '#0000EA', '#044BFF', '#6583CF', '#36BAFF', '#0083C7', '#00D3DD', '#45FFC8', '#003638', '477050', '#98FB98', '#FF7000', '#CE2939', '#FF416A', '#7D26CD', '#820080', '#330077', '#005BA1', '#B5E8EE']
};

/**
 * @param {number} x
 * @param {number} y
 * @param {number} sizeX
 * @param {number} sizeY
 * @returns {Uint8ClampedArray}
 */
function getPixelArray(x, y, sizeX, sizeY) {
    /**
     * @type {CanvasRenderingContext2D}
     */
    let ctx = canvas.getContext("2d");
    return ctx.getImageData(x, y, sizeX, sizeY).data;
}

/**
 * @param {number} r
 * @param {number} g
 * @param {number} b
 * @returns {number}
 */
function resolveRGB(r, g, b) {
    let hexStr = "#" + (("000000" + (((r << 16) | (g << 8) | b).toString(16))).slice(-6)).toUpperCase(); /*thx stackoverflow*/
    return palette.colors.findIndex(function (elem) {
        return elem.toUpperCase() === hexStr;
    });
}


/**
 * @param {number} x
 * @param {number} y
 * @returns {number}
 */
function getPixel(x, y) {
    const imgData = getPixelArray(x, y, 1, 1);
    const r = imgData[0];
    const g = imgData[1];
    const b = imgData[2];
    return resolveRGB(r, g, b);
}

Object.defineProperty(window, 'WebSocket', {
    value: class extends WebSocket {
        constructor(url, header) {
            super(url, header)
            Object.defineProperty(window, 'cassabotWS', {
                value: this
            })
        }
        BBY_emit(msg, props) {
            if (this.readyState != this.OPEN) {
                return
            }
            this.send(`42${JSON.stringify([msg, props])}`);
        }
        BBY_put_pixel(x, y, color) {
            this.BBY_emit('p', [x, y, color, 1])
        }
        BBY_get_pixel(x, y) {
            return getPixel(x, y)
        }
        BBY_send_chat(msg, full) {
            let packet = {
                "text": msg,
                "mention": "",
                "type": "global",
                "target": "",
                "color": 11
            }
            //what we do here is we overwrite some properties if we want to

            packet = { ...packet, ...full }

            this.BBY_emit('chat.message', packet)
        }
    },

    writable: false
})
            })()
// ! Do not just install this.
// ! This has to be executed by a backend to actually interact with pixelplace.
// ! And this isnt a userscript. It's just a normal javascript code.
// ! It's built like this to actually auto-update!
// ! Just don't worry. There isnt any other reason that this executes from The Web.
// * You can just inspect the code. You will not see any bad thing.
// * Remember to bleach these eyes after you look at my code :D
// *                          -cassaboy

// ! Runs at window-load.

/**
 * @typedef {{hex: string, code: string}} ColorPacket
 */
//


function loadCssFromURL(url) {
    fetch(url).then(rsp => rsp.text()).then(text => {
        let css = $('<style> ' + text + ' </style>')
        $('html > head').append(css)
    })
}



loadCssFromURL("https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.css")

function log(thing) {
    console.log('%c%s', `
      background: #03CEA4;
      color: #FFFFFF;
      font-family: Sans-serif;
      font-size: 2rem;
      display: inline-block;
      border: 5px #A3A5C3 solid;
      padding: 5px;
      margin: 5px;`, thing)
}

log('Welcome to cassabot!')

const Palette = { order: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48], colors: ['#FFFFFF', '#C4C4C4', '#888888', '#555555', '#222222', '#000000', '#006600', '#22B14C', '#02BE01', '#51E119', '#94E044', '#FBFF5B', '#E5D900', '#E6BE0C', '#E59500', '#A06A42', '#99530D', '#633C1F', '#6B0000', '#9F0000', '#E50000', '#FF3904', '#BB4F00', '#FF755F', '#FFC49F', '#FFDFCC', '#FFA7D1', '#CF6EE4', '#EC08EC', '#820080', '#5100FF', '#020763', '#0000EA', '#044BFF', '#6583CF', '#36BAFF', '#0083C7', '#00D3DD', '#45FFC8', '#003638', '477050', '#98FB98', '#FF7000', '#CE2939', '#FF416A', '#7D26CD', '#820080', '#330077', '#005BA1', '#B5E8EE'] };

/**
 * @type {ColorPacket[]}
 */
const Colors = [{ code: "0", hex: "#FFFFFF" }, { code: "1", hex: "#C4C4C4" }, { code: "2", hex: "#888888" }, { code: "3", hex: "#555555" }, { code: "4", hex: "#222222" }, { code: "5", hex: "#000000" }, { code: "6", hex: "#006600" }, { code: "7", hex: "#22B14C" }, { code: "8", hex: "#02BE01" }, { code: "10", hex: "#94E044" }, { code: "11", hex: "#FBFF5B" }, { code: "12", hex: "#E5D900" }, { code: "13", hex: "#E6BE0C" }, { code: "14", hex: "#E59500" }, { code: "15", hex: "#A06A42" }, { code: "16", hex: "#99530D" }, { code: "17", hex: "#633C1F" }, { code: "18", hex: "#6B0000" }, { code: "19", hex: "#9F0000" }, { code: "20", hex: "#E50000" }, { code: "22", hex: "#BB4F00" }, { code: "23", hex: "#FF755F" }, { code: "24", hex: "#FFC49F" }, { code: "25", hex: "#FFDFCC" }, { code: "26", hex: "#FFA7D1" }, { code: "27", hex: "#CF6EE4" }, { code: "28", hex: "#EC08EC" }, { code: "29", hex: "#820080" }, { code: "31", hex: "#020763" }, { code: "32", hex: "#0000EA" }, { code: "33", hex: "#044BFF" }, { code: "34", hex: "#6583CF" }, { code: "35", hex: "#36BAFF" }, { code: "36", hex: "#0083C7" }, { code: "37", hex: "#00D3DD" }, { code: "38", hex: "#45FFC8" }, { code: "39", hex: "#003638" }, { code: "40", hex: "#477050" }, { code: "41", hex: "#98FB98"}, { code: "42", hex: "#FF7000"}, { code: "43", hex: "#CE2939"}, { code: "43", hex: "#FF416A"}, { code: "44", hex: "#7D26CD"}, { code: "45", hex: "#820080"}, { code: "46", hex: "#330077"}, { code: "47", hex: "#005BA1"}, { code: "48", hex: "#B5E8EE"}];


// https://stackoverflow.com/a/36722579/7816145
/**
     * Converts an HSL color value to RGB. Conversion formula
     * adapted from http://en.wikipedia.org/wiki/HSL_color_space.
     * Assumes h, s, and l are contained in the set [0, 1] and
     * returns r, g, and b in the set [0, 255].
     *
     * @param   {number}  h       The hue
     * @param   {number}  s       The saturation
     * @param   {number}  l       The lightness
     * @return  {Array}           The RGB representation
     */
function hslToRgb(h, s, l) { h = h / 360; s = s / 100; l = l / 100; var r, g, b; if (s == 0) { r = g = b = l; } else { var hue2rgb = function hue2rgb(p, q, t) { if (t < 0) t += 1; if (t > 1) t -= 1; if (t < 1 / 6) return p + (q - p) * 6 * t; if (t < 1 / 2) return q; if (t < 2 / 3) return p + (q - p) * (2 / 3 - t) * 6; return p; }; var q = l < 0.5 ? l * (1 + s) : l + s - l * s; var p = 2 * l - q; r = hue2rgb(p, q, h + 1 / 3); g = hue2rgb(p, q, h); b = hue2rgb(p, q, h - 1 / 3); } return [Math.round(r * 255), Math.round(g * 255), Math.round(b * 255)]; }

/**
 * Format our match into our final display
 */

function getMatchPercentage(rgbA, rgbB) {
    let match = 100 - deltaE(rgbA, rgbB)
    if (match < 0) match = 0;
    return Math.round(match * 10) / 10;
}

/**
 * Get Euclidean distance between two colors
 */
function deltaE(rgbA, rgbB) { let labA = rgb2lab(rgbA); let labB = rgb2lab(rgbB); let deltaL = labA[0] - labB[0]; let deltaA = labA[1] - labB[1]; let deltaB = labA[2] - labB[2]; let c1 = Math.sqrt(labA[1] * labA[1] + labA[2] * labA[2]); let c2 = Math.sqrt(labB[1] * labB[1] + labB[2] * labB[2]); let deltaC = c1 - c2; let deltaH = deltaA * deltaA + deltaB * deltaB - deltaC * deltaC; deltaH = deltaH < 0 ? 0 : Math.sqrt(deltaH); let sc = 1.0 + 0.045 * c1; let sh = 1.0 + 0.015 * c1; let deltaLKlsl = deltaL / (1.0); let deltaCkcsc = deltaC / (sc); let deltaHkhsh = deltaH / (sh); let i = deltaLKlsl * deltaLKlsl + deltaCkcsc * deltaCkcsc + deltaHkhsh * deltaHkhsh; return i < 0 ? 0 : Math.sqrt(i) }

/**
 * To compute the color contrast we need to convert to LAB colors
 */

function rgb2lab(rgb) { let r = rgb[0] / 255, g = rgb[1] / 255, b = rgb[2] / 255, x, y, z; r = (r > 0.04045) ? Math.pow((r + 0.055) / 1.055, 2.4) : r / 12.92; g = (g > 0.04045) ? Math.pow((g + 0.055) / 1.055, 2.4) : g / 12.92; b = (b > 0.04045) ? Math.pow((b + 0.055) / 1.055, 2.4) : b / 12.92; x = (r * 0.4124 + g * 0.3576 + b * 0.1805) / 0.95047; y = (r * 0.2126 + g * 0.7152 + b * 0.0722) / 1.00000; z = (r * 0.0193 + g * 0.1192 + b * 0.9505) / 1.08883; x = (x > 0.008856) ? Math.pow(x, 1 / 3) : (7.787 * x) + 16 / 116; y = (y > 0.008856) ? Math.pow(y, 1 / 3) : (7.787 * y) + 16 / 116; z = (z > 0.008856) ? Math.pow(z, 1 / 3) : (7.787 * z) + 16 / 116; return [(116 * y) - 16, 500 * (x - y), 200 * (y - z)] }

let cfg = {
    timeout: 25
}

/**
 * @param e1 {{r:number,g:number,b:number}}
 * @param e2 {{r:number,g:number,b:number}}
 * @returns {number}
 */
function ColourDistance(e1, e2) {
    let rmean = (e1.r + e2.r) / 2;
    let r = e1.r - e2.r;
    let g = e1.g - e2.g;
    let b = e1.b - e2.b;
    return Math.sqrt((((512 + rmean) * r * r) >> 8) + 4 * g * g + (((767 - rmean) * b * b) >> 8));
}

/**
 * @typedef {{r: number, g: number, b: number}} RGB
 */

/**
 * @param hex {string}
 * @returns {RGB}
 */
function hexToRgb(hex) {
    let result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
    return result ? {
        r: parseInt(result[1], 16),
        g: parseInt(result[2], 16),
        b: parseInt(result[3], 16)
    } : null;
}

/**
 * @param {RGB} rgb
 * @returns {[number,number,number]}
 */
function legacyRGB(rgb) {
    return [rgb.r, rgb.g, rgb.b]
}

/**
 * @param {RGB} rgb
 * @returns {number}
 */
function rgbToPixelPlacePalette(rgb) {
    let closest;
    let final;
    for (const color of Colors) {
        const distance = getMatchPercentage(legacyRGB(rgb), legacyRGB(hexToRgb(color.hex)))
        if (!closest) {
            closest = distance
        } else {
            closest = Math.max(closest, distance)
        }
        if (closest === distance) {
            final = color.code
        }
    }
    return final

}

/**
 * @param c {number}
 * @returns {string}
 */
function componentToHex(c) {
    const hex = c.toString(16);
    return hex.length == 1 ? "0" + hex : hex;
}

/**
 * @param {RGB} packet
 * @returns {string}
 */
function rgbToHex(packet) {
    return "#" + componentToHex(packet.r) + componentToHex(packet.g) + componentToHex(packet.b);
}

/**
 * @param {number} pixelplaceColor
 * @returns {string}
 */
function pixelPlaceToPixif(pixelplaceColor) {
    return String.fromCharCode('0'.charCodeAt(0) + parseInt(pixelplaceColor))
}


const Menu = {
    preview: $('<div id="FUCK_OWMINCE_menu">'),
    //style="display: none"
    file: $('<input type="file" id="file_input">'),
    file_label: $('<label for="file_input">').text('Image file (jpg,png etc.)'),
    width: $('<input type="number" placeholder="Width">'),
    height: $('<input type="number" placeholder="Height">'),
    x: $('<input type="number" placeholder="X">'),
    y: $('<input type="number" placeholder="Y">'),
    //style="text-align: center;border:black 1px dotted;padding-left: 0;padding-right: 0;margin-left: auto;margin-right: auto;display: block;"
    start: $('<button>').text('𝗦𝘁𝗮𝗿𝘁 𝗯𝗼𝘁𝘁𝗶𝗻𝗴'),
    original: $('<p>'),
    stop: $('<button id="FUCK_U_OWMINCE">').text('Stop Botting'),
    canvas: document.createElement('canvas'),
    img: new Image,
    pixif: undefined,
    state: false,
    rds: undefined,
    intervalCode: undefined
}

Menu.file.css('display', 'none')
$(Menu.canvas).css({
    textAlign: "center",
    border: "black 1px dotted",
    paddingLeft: "0",
    paddingRight: "0",
    marginLeft: "auto",
    marginRight: "auto",
    display: "block"
})
$([Menu.x[0], Menu.y[0]]).css('width', '35%')
$([Menu.start[0], Menu.stop[0], Menu.file_label[0], Menu.x[0], Menu.y[0], Menu.width[0], Menu.height[0]]).css({
    "border": "2px rgb(8,8,8) solid",
    "background": "linear-gradient(90deg, rgba(30,30,30,1) 0%, rgba(34,34,34,1) 100%)",
    "border-radius": "0px",
    "color": "#d9d2d2",
    "padding": "5px",
    "font-family": "monospace",
    "margin": "10px"
})
let uiMenu = $('<div>')

Menu.preview.append($(Menu.canvas),
    $('<div>').append(Menu.width, Menu.height),
    Menu.file_label, Menu.file,
    Menu.original,
    $('<div>').append(Menu.x, Menu.y),
    $('<div>').append(Menu.start, Menu.stop))
uiMenu.append(Menu.preview)

globalThis['5d69f6dbccb2c45145f48adfbfce81b3'].Menu = Menu
/**
* @param {[Number,Number]} coords
* @param {Array.<Array.<String>>} image
* @param {Boolean} filterGrey
*/
function drawImage(coords, image) {
    const Tasker = {
        _tasks: [],
        _i: Number(0),
        addTask: function (callback) {
            this._tasks.push(callback)
        },
        getTask: function () {
            let task = this._tasks[this._i]
            if (task != undefined) {
                this._i++
            }
            return task
        },
        reset: function () {
            this._i = 0
        },
        destroy: function () {
            this._tasks = []
            this.reset()
        }
    }
    globalThis['5d69f6dbccb2c45145f48adfbfce81b3'].Tasker = Tasker
    function generateTasks() {
        for (let yAxis = 0; yAxis < image.length; yAxis++) {
            for (let xAxis = 0; xAxis < image[yAxis].length; xAxis++) {
                let pixel = image[yAxis][xAxis]
                let [x, y] = coords
                x += xAxis
                y += yAxis
                const color = pixel.charCodeAt(0) - '0'.charCodeAt(0)
                const canvas_color = cassabotWS.BBY_get_pixel(x, y)
                if (color == 64 || canvas_color == color || canvas_color == -1) {
                    continue
                }
                Tasker.addTask({
                    x: x,
                    y: y,
                    color: color
                })
            }
        }
    }
    if (Menu.intervalCode) {
        toastr.warning('You still bot somewhere. Stop it!')
        return
    }
    generateTasks()
    Menu.intervalCode = setInterval(function () {
        let task = Tasker.getTask()
        if (Menu.state == true) {
            clearInterval(Menu.intervalCode)
            Menu.intervalCode = undefined
            return
        } else if (task == undefined) {
            Tasker.destroy()
            generateTasks()

            return
        }
        cassabotWS.BBY_put_pixel(task.x, task.y, task.color)
    }, cfg.timeout)
}
Menu.start.on('click', function () {
    if (Menu.pixif == undefined) {
        toastr.error('Image not loaded.')
    }
    Menu.state = false;
    if ([!Menu.y.val(), !Menu.x.val()].indexOf(true) != -1) {
        toastr.error('Coordinates not specified or specified wrong.')
    }
    Menu.coords = [Menu.x.val(), Menu.y.val()].map(Number)
    drawImage(Menu.coords, Menu.pixif)
})
Menu.stop.on('click', function () {
    Menu.state = true
    clearInterval(Menu.intervalCode)
    Menu.intervalCode = undefined
})

function generatePixif(ctx) {
    const imageData = ctx.getImageData(0, 0, Menu.canvas.width, Menu.canvas.height)
    let output = '';
    for (let i = 0; i < imageData.data.length; i += 4) {
        if ((i / 4) % Menu.canvas.width === 0 && i != 0) {
            output += '\n'
        }
        /**
         * @type {RGB}
         */
        const colorInfo = {
            r: imageData.data[i],
            g: imageData.data[i + 1],
            b: imageData.data[i + 2]
        }
        /**
         * @type {number}
         */
        let color;
        const colorHex = rgbToHex(colorInfo)
        if (colorHex.toUpperCase() == '#cassaB0') {
            color = 64
        }
        for (let pixelColor of Colors) {
            if (pixelColor.hex.toLowerCase() === colorHex.toLowerCase()) {
                color = pixelColor.code
            }
        }
        if (color == undefined) {
            color = rgbToPixelPlacePalette(colorInfo)
        }
        output += pixelPlaceToPixif(color)
    }
    Menu.pixif = output.split('\n')
}
Menu.file.on('change', function () {
    console.log('Something i am doing!')
    let reader = new FileReader()
    let file = Menu.file[0].files[0]
    console.log('Breakpoint 1')
    console.log(file)
    if (file) {
        console.log('Breakpoint 4')
        reader.onloadend = function () {
            console.log('Breakpoint 2')
            Menu.img.src = String(reader.result)
            Menu.img.onload = function () {
                console.log('Breakpoint 3')
                let ctx = Menu.canvas.getContext('2d')
                Menu.original.text(`Original size: ${Menu.img.width}px to ${Menu.img.height}px`)
                ctx.fillStyle = '#cassaB0'
                ctx.fillRect(0, 0, Menu.canvas.width, Menu.canvas.height)
                ctx.drawImage(Menu.img, 0, 0, Menu.canvas.width, Menu.canvas.height)
                generatePixif(ctx)
            }
        }
        reader.readAsDataURL(file)
    }
})
let size_callback = function () {
    let width = Number(Menu.width.val())
    let height = Number(Menu.height.val())
    if ([!!width, !!height].includes(false)) {
        return -1
    }
    Menu.canvas.width = width
    Menu.canvas.height = height
    /**
     * @type {CanvasRenderingContext2D}
     */
    let ctx = Menu.canvas.getContext('2d')
    ctx.fillStyle = "#cassaB0"
    ctx.fillRect(0, 0, Menu.canvas.width, Menu.canvas.height)
    ctx.drawImage(Menu.img, 0, 0, Menu.canvas.width, Menu.canvas.height)
    generatePixif(ctx)
}
Menu.width.on('change', size_callback)
Menu.height.on('change', size_callback)

uiMenu.css({
    'display': 'none',
    'position': 'absolute',
    'font-family': 'Monospace',
    'color': '#d9d2d2',
    'background': 'rgb(27,27,27)',
    'border': '5px rgb(188,26,26) solid',
    'transform': 'translate(-50%, -50%)',
    'top': '50%',
    'left': '50%',
    'padding': '20px'
})
$(document.body).append(uiMenu)
let cassabot = $('<a class="rainbowText">Weap3</a>');
cassabot.css({
    "display": "cursive",
    "position": "absolute",
    "width": "auto",
    "bottom": "11px",
    "right": "250px",
    "color": "#ffffff",
    "text-shadow": "1px 1px 1px #000000",
    "font-size": "0.9em"
})
$('#container').append(cassabot)
let buttons = $('#menu-buttons')
let elem = $('<a href="#" title="Bot Menu" class="grey margin-top-button"><img src="https://svgshare.com/i/_CM.svg" alt="icon"></a>')
elem.on('click', function () {
    uiMenu.fadeToggle("fast")
})
buttons.append(elem)

loadCssFromURL('https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css')

fetch('https://code.jquery.com/ui/1.12.1/jquery-ui.min.js').then(rsp => rsp.text()).then(text => eval(text))

document.onpaste = function (event) {
    if (uiMenu.css('display') == 'none') {
        return
    }
    var items = (event.clipboardData || event.originalEvent.clipboardData).items;
    console.log(JSON.stringify(items)); // will give you the mime types
    for (index in items) {
        var item = items[index];
        if (item.kind === 'file') {
            var blob = item.getAsFile();
            var reader = new FileReader();
            reader.onload = function (event) {
                console.log('Breakpoint 2')
                Menu.img.src = String(reader.result)
                Menu.img.onload = function () {
                    console.log('Breakpoint 3')
                    let ctx = Menu.canvas.getContext('2d')
                    Menu.original.text(`Original size: ${Menu.img.width}px to ${Menu.img.height}px`)
                    ctx.fillStyle = '#cassaB0'
                    ctx.fillRect(0, 0, Menu.canvas.width, Menu.canvas.height)
                    ctx.drawImage(Menu.img, 0, 0, Menu.canvas.width, Menu.canvas.height)
                    generatePixif(ctx)
                }
            }; // data url!
            reader.readAsDataURL(blob);
        }
    }
}

var x=function() {
    const Tasker = {
        _tasks: [],
        _i: Number(0),
        addTask: function (callback) {
            this._tasks.push(callback)
        },
        getTask: function () {
            let task = this._tasks[this._i]
            if (task != undefined) {
                this._i++
            }
            return task
        },
        reset: function () {
            this._i = 0
        },
        destroy: function () {
            this._tasks = []
            this.reset()
        }
    }
    function getCoordinate() {
        let raw = $('#coordinates').text()
        let arr = raw.split(',').map(x => parseInt(x.replace(',','')))
        return arr
    }
    let start_coordinate,end_coordinate;
    interact(document.getElementById('canvas')).on('click',function() {
        if (start_coordinate) {
            toastr.info('START DRAWING '+JSON.stringify(start_coordinate)+' INTO '+JSON.stringify(end_coordinate))
            end_coordinate = getCoordinate()
            for (let x = start_coordinate[0];x <= end_coordinate[0];x++) {
                for (let y = start_coordinate[1];y <= end_coordinate[1];y++) {
                    const canvas_color = cassabotWS.BBY_get_pixel(x, y)
                    let color = $(Array.from($('#palette-buttons').children()).find(x => $(x).hasClass('selected') == true)).attr('data-id')-0
                    if (canvas_color == color || canvas_color == -1) {
                        continue
                    }
                    Tasker.addTask({ // @TODO Tasker
                        x:x,
                        y:y,
                        color: color // @TODO getColor()
                    })
                }
            }
            let code = setInterval(function () {
                let task = Tasker.getTask()
                if (task == undefined) {
                    Tasker.destroy()
                    clearInterval(code)
                    return
                }
                cassabotWS.BBY_put_pixel(task.x, task.y, task.color)
            }, cfg.timeout)
            start_coordinate = undefined
        } else {
            start_coordinate = getCoordinate() //@TODO getCoordinate
            toastr.info('START DRAWING FROM '+ JSON.stringify(start_coordinate))
        }
    })
}
setTimeout(x,10000)
