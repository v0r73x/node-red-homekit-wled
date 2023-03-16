# node-red-homekit-wled
an json API controlled flow which allows to set WLED in HomeKit with 1 FX switch.

Requirements I had:

- color must be bidirectional controlled by flow (When inputs on WLED Gui it will update Homekit state as well 
- own node red dashboard control possibility 
- Siri Assistant WHITHOUT falling into state RED !!! (most important for me ;) ) 
- Usebility with Sound Reactive WLEDs to trigger by switch the Sound Reaction FX (FX:132) called gravicenter which is also possible to trigger by Siri

Just import whole code into Node Red. You need some packages as reqirement...

flow:

![image](https://user-images.githubusercontent.com/48632087/225753708-8671dfbb-b18d-432d-9242-a918e97e2181.png)

_______________________________________________________________________________________________________________________________________________________

[
    {
        "id": "20061a0525813035",
        "type": "tab",
        "label": "WLED.OFFICE.FX",
        "disabled": true,
        "info": ""
    },
    {
        "id": "4f339acb82b4fa4f",
        "type": "ui_colour_picker",
        "z": "20061a0525813035",
        "name": "",
        "label": "Primary Color",
        "group": "5972d9ad77220186",
        "format": "rgb",
        "outformat": "object",
        "showSwatch": true,
        "showPicker": false,
        "showValue": false,
        "showHue": false,
        "showAlpha": false,
        "showLightness": true,
        "square": "false",
        "dynOutput": "false",
        "order": 1,
        "width": "4",
        "height": "1",
        "passthru": false,
        "topic": "",
        "topicType": "str",
        "className": "",
        "x": 820,
        "y": 160,
        "wires": [
            [
                "35347868cafaece4",
                "34b322a73d2df9f1"
            ]
        ]
    },
    {
        "id": "529a5bc82d66ef72",
        "type": "ui_colour_picker",
        "z": "20061a0525813035",
        "name": "",
        "label": "Secondary Color",
        "group": "5972d9ad77220186",
        "format": "rgb",
        "outformat": "object",
        "showSwatch": true,
        "showPicker": false,
        "showValue": false,
        "showHue": false,
        "showAlpha": false,
        "showLightness": true,
        "square": "false",
        "dynOutput": "false",
        "order": 2,
        "width": "4",
        "height": "1",
        "passthru": false,
        "topic": "",
        "topicType": "str",
        "className": "",
        "x": 830,
        "y": 200,
        "wires": [
            [
                "d8ee5e0717f526b4"
            ]
        ]
    },
    {
        "id": "8f771915458bc72c",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 180,
        "wires": []
    },
    {
        "id": "34b322a73d2df9f1",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 1030,
        "y": 120,
        "wires": []
    },
    {
        "id": "8e14d654188ae8b1",
        "type": "config",
        "z": "20061a0525813035",
        "name": "Active WLED IP",
        "properties": [
            {
                "p": "wled_ip",
                "pt": "flow",
                "to": "192.168.178.119",
                "tot": "str"
            }
        ],
        "active": true,
        "x": 140,
        "y": 40,
        "wires": []
    },
    {
        "id": "931a9ce7bf9638bd",
        "type": "config",
        "z": "20061a0525813035",
        "d": true,
        "name": "Active WLED MQTT Topic",
        "properties": [
            {
                "p": "wled_topic",
                "pt": "flow",
                "to": "wled/roof",
                "tot": "str"
            }
        ],
        "active": true,
        "x": 170,
        "y": 80,
        "wires": []
    },
    {
        "id": "f5c1c87d49bd869a",
        "type": "http request",
        "z": "20061a0525813035",
        "name": "",
        "method": "GET",
        "ret": "obj",
        "paytoqs": false,
        "url": "",
        "tls": "",
        "persist": false,
        "proxy": "",
        "authType": "",
        "x": 330,
        "y": 1120,
        "wires": [
            [
                "01b2f8038146ec9e"
            ]
        ]
    },
    {
        "id": "18a7e131123ac5c3",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 550,
        "y": 1340,
        "wires": []
    },
    {
        "id": "50546cc83e36ac02",
        "type": "template",
        "z": "20061a0525813035",
        "name": "Get JSON Status",
        "field": "url",
        "fieldType": "msg",
        "format": "handlebars",
        "syntax": "mustache",
        "template": "http://{{flow.wled_ip}}/json",
        "output": "str",
        "x": 570,
        "y": 980,
        "wires": [
            [
                "6ec2f8b1ee552ff2",
                "18425db197cb1e31"
            ]
        ]
    },
    {
        "id": "e56ee39e01f0fc71",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Store Effects Array",
        "func": "flow.set('effects', msg.payload)\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 570,
        "y": 1260,
        "wires": [
            []
        ]
    },
    {
        "id": "565015a46e76c9ce",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Store Palettes Array",
        "func": "flow.set('palettes', msg.payload)\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 580,
        "y": 1380,
        "wires": [
            []
        ]
    },
    {
        "id": "82800acc52eb170d",
        "type": "ui_dropdown",
        "z": "20061a0525813035",
        "name": "",
        "label": "Effects",
        "tooltip": "",
        "place": "Select option",
        "group": "5972d9ad77220186",
        "order": 8,
        "width": "6",
        "height": "1",
        "passthru": false,
        "multiple": false,
        "options": [
            {
                "label": "",
                "value": "",
                "type": "str"
            }
        ],
        "payload": "",
        "topic": "",
        "topicType": "str",
        "className": "",
        "x": 790,
        "y": 280,
        "wires": [
            [
                "99b50a94ffb7d037"
            ]
        ]
    },
    {
        "id": "739eabf79ebf3df6",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Invert Array",
        "func": "var effects = msg.payload;\nmsg.paylod = null;\nmsg.options = [];\nfor (var i=0; i<effects.length; i++) {\n    var t = {};\n    t[effects[i]] = i;\n    msg.options.push(t);\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 550,
        "y": 1300,
        "wires": [
            [
                "82800acc52eb170d"
            ]
        ]
    },
    {
        "id": "d9aeaae159f9b2a5",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 550,
        "y": 1220,
        "wires": []
    },
    {
        "id": "e4a1bb0f36817830",
        "type": "ui_dropdown",
        "z": "20061a0525813035",
        "name": "",
        "label": "Palettes",
        "tooltip": "",
        "place": "Select option",
        "group": "5972d9ad77220186",
        "order": 9,
        "width": "6",
        "height": "1",
        "passthru": false,
        "multiple": false,
        "options": [
            {
                "label": "",
                "value": "",
                "type": "str"
            }
        ],
        "payload": "",
        "topic": "",
        "topicType": "str",
        "className": "",
        "x": 800,
        "y": 320,
        "wires": [
            [
                "6cf1b294fcb3d50f"
            ]
        ]
    },
    {
        "id": "4bba294bdb4b6010",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Invert Array",
        "func": "var palettes = msg.payload;\nmsg.paylod = null;\nmsg.options = [];\nfor (var i=0; i<palettes.length; i++) {\n    var t = {};\n    t[palettes[i]] = i;\n    msg.options.push(t);\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 550,
        "y": 1420,
        "wires": [
            [
                "e4a1bb0f36817830"
            ]
        ]
    },
    {
        "id": "ed5f75ddba646f65",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract FX Index",
        "func": "msg.payload = msg.payload.seg[0].fx;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 380,
        "y": 280,
        "wires": [
            [
                "82800acc52eb170d",
                "5d03bf7193b4ac4b"
            ]
        ]
    },
    {
        "id": "ad7776af1e3e69e8",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Palette Index",
        "func": "msg.payload = msg.payload.seg[0].pal;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 400,
        "y": 320,
        "wires": [
            [
                "e4a1bb0f36817830",
                "237cda93bf9d3684"
            ]
        ]
    },
    {
        "id": "ca5855770d303367",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract FX Speed",
        "func": "msg.payload = msg.payload.seg[0].sx;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 390,
        "y": 360,
        "wires": [
            [
                "d8b44c2d73327572",
                "6f3293a4596aaeb5"
            ]
        ]
    },
    {
        "id": "be1cbbb9fa4120c4",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract FX Intensity",
        "func": "msg.payload = msg.payload.seg[0].ix;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 390,
        "y": 400,
        "wires": [
            [
                "2a6a2a7a1550ed6b",
                "6e971c8f57298c89"
            ]
        ]
    },
    {
        "id": "d8b44c2d73327572",
        "type": "ui_slider",
        "z": "20061a0525813035",
        "name": "",
        "label": "FX Speed",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 10,
        "width": 0,
        "height": 0,
        "passthru": true,
        "outs": "end",
        "topic": "",
        "topicType": "str",
        "min": 0,
        "max": "255",
        "step": 1,
        "className": "",
        "x": 800,
        "y": 360,
        "wires": [
            [
                "e15cf5ebaf51a2d4"
            ]
        ]
    },
    {
        "id": "2a6a2a7a1550ed6b",
        "type": "ui_slider",
        "z": "20061a0525813035",
        "name": "",
        "label": "FX Intensity",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 11,
        "width": 0,
        "height": 0,
        "passthru": true,
        "outs": "end",
        "topic": "",
        "topicType": "str",
        "min": 0,
        "max": "255",
        "step": 1,
        "className": "",
        "x": 810,
        "y": 400,
        "wires": [
            [
                "c5e7bb6cea6bdcf6"
            ]
        ]
    },
    {
        "id": "d93964e1a51f8aef",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Global Brightness",
        "func": "msg.payload = msg.payload.bri;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 410,
        "y": 440,
        "wires": [
            [
                "3e79aa6cd34102c7",
                "33de10e90d8c104d"
            ]
        ]
    },
    {
        "id": "3e79aa6cd34102c7",
        "type": "ui_slider",
        "z": "20061a0525813035",
        "name": "",
        "label": "Global Brightness",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 12,
        "width": "0",
        "height": "0",
        "passthru": true,
        "outs": "end",
        "topic": "",
        "topicType": "str",
        "min": 0,
        "max": "255",
        "step": 1,
        "className": "",
        "x": 830,
        "y": 440,
        "wires": [
            [
                "a64d4c43d1abbd1c"
            ]
        ]
    },
    {
        "id": "5d03bf7193b4ac4b",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 260,
        "wires": []
    },
    {
        "id": "237cda93bf9d3684",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 300,
        "wires": []
    },
    {
        "id": "6e971c8f57298c89",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 380,
        "wires": []
    },
    {
        "id": "6f3293a4596aaeb5",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 340,
        "wires": []
    },
    {
        "id": "33de10e90d8c104d",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 420,
        "wires": []
    },
    {
        "id": "7023332786ef9284",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "x": 970,
        "y": 1080,
        "wires": []
    },
    {
        "id": "7173090fa6a31236",
        "type": "link out",
        "z": "20061a0525813035",
        "name": "WLED JSON State",
        "links": [
            "1595ab509977c113"
        ],
        "x": 1195,
        "y": 1120,
        "wires": []
    },
    {
        "id": "1595ab509977c113",
        "type": "link in",
        "z": "20061a0525813035",
        "name": "WLED JSON State out",
        "links": [
            "7173090fa6a31236"
        ],
        "x": 55,
        "y": 120,
        "wires": [
            [
                "6f5960a0d23f18c2"
            ]
        ]
    },
    {
        "id": "d1134e8162368efa",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Power State",
        "func": "msg.payload = msg.payload.on;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 400,
        "y": 480,
        "wires": [
            [
                "23495075960d2401",
                "96f61baf8d57bf6f"
            ]
        ]
    },
    {
        "id": "23495075960d2401",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 610,
        "y": 460,
        "wires": []
    },
    {
        "id": "96f61baf8d57bf6f",
        "type": "ui_switch",
        "z": "20061a0525813035",
        "name": "",
        "label": "Power",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 4,
        "width": "3",
        "height": "1",
        "passthru": false,
        "decouple": "true",
        "topic": "",
        "topicType": "str",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "animate": true,
        "className": "",
        "x": 791,
        "y": 480,
        "wires": [
            [
                "08f3c178fef1717c",
                "83aa9e6a.6ac9e"
            ]
        ]
    },
    {
        "id": "a49da06e1e113b75",
        "type": "mqtt in",
        "z": "20061a0525813035",
        "d": true,
        "name": "",
        "topic": "wled/sample/v",
        "qos": "2",
        "datatype": "auto",
        "broker": "",
        "nl": false,
        "rap": false,
        "rh": "0",
        "inputs": 0,
        "x": 120,
        "y": 980,
        "wires": [
            [
                "aba1b8a81745c9d8"
            ]
        ]
    },
    {
        "id": "035c0a95c6788b1b",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Color 1",
        "func": "msg.payload = {\n    \"r\":msg.payload.seg[0].col[0][0],\n    \"g\":msg.payload.seg[0].col[0][1],\n    \"b\":msg.payload.seg[0].col[0][2],\n    \"a\":255\n};\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 380,
        "y": 160,
        "wires": [
            [
                "622af01f1b3883f6",
                "4f339acb82b4fa4f"
            ]
        ]
    },
    {
        "id": "622af01f1b3883f6",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 610,
        "y": 140,
        "wires": []
    },
    {
        "id": "a72b4716853fe44e",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 220,
        "wires": []
    },
    {
        "id": "c49c2e97545f3c6d",
        "type": "link out",
        "z": "20061a0525813035",
        "name": "JSON API",
        "links": [
            "4c463f8cb01dbdea"
        ],
        "x": 1235,
        "y": 160,
        "wires": []
    },
    {
        "id": "95b09c031fb68839",
        "type": "template",
        "z": "20061a0525813035",
        "name": "JSON API URL",
        "field": "url",
        "fieldType": "msg",
        "format": "handlebars",
        "syntax": "mustache",
        "template": "http://{{flow.wled_ip}}/json/state",
        "output": "str",
        "x": 260,
        "y": 920,
        "wires": [
            [
                "3ade75303b1043e2"
            ]
        ]
    },
    {
        "id": "4c463f8cb01dbdea",
        "type": "link in",
        "z": "20061a0525813035",
        "name": "",
        "links": [
            "c49c2e97545f3c6d"
        ],
        "x": 115,
        "y": 920,
        "wires": [
            [
                "95b09c031fb68839"
            ]
        ]
    },
    {
        "id": "1f2d0f60ee5f4fa1",
        "type": "http request",
        "z": "20061a0525813035",
        "name": "",
        "method": "POST",
        "ret": "obj",
        "paytoqs": "ignore",
        "url": "",
        "tls": "",
        "persist": false,
        "proxy": "",
        "insecureHTTPParser": false,
        "authType": "",
        "senderr": false,
        "headers": [],
        "x": 810,
        "y": 920,
        "wires": [
            [
                "cd8ef5b18d4f4a19"
            ]
        ]
    },
    {
        "id": "cd8ef5b18d4f4a19",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 990,
        "y": 920,
        "wires": []
    },
    {
        "id": "35347868cafaece4",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Color 1",
        "func": "var color = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"col\": [\n    [color.r,color.g,color.b],\n    [],\n    []\n    ]};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1030,
        "y": 160,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "3ade75303b1043e2",
        "type": "json",
        "z": "20061a0525813035",
        "name": "",
        "property": "payload",
        "action": "",
        "pretty": false,
        "x": 430,
        "y": 920,
        "wires": [
            [
                "42d0c2b377121952",
                "2be269b4b7161fd2"
            ]
        ]
    },
    {
        "id": "57048ce993979ff9",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Color 2",
        "func": "msg.payload = {\n    \"r\":msg.payload.seg[0].col[1][0],\n    \"g\":msg.payload.seg[0].col[1][1],\n    \"b\":msg.payload.seg[0].col[1][2],\n    \"a\":255\n};\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 380,
        "y": 200,
        "wires": [
            [
                "529a5bc82d66ef72",
                "8f771915458bc72c"
            ]
        ]
    },
    {
        "id": "d8ee5e0717f526b4",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Color 2",
        "func": "var color = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"col\": [\n    [],\n    [color.r,color.g,color.b],\n    []\n]};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1030,
        "y": 200,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "69a3d5ceff8c4e5c",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Color 3",
        "func": "msg.payload = {\n    \"r\":msg.payload.seg[0].col[2][0],\n    \"g\":msg.payload.seg[0].col[2][1],\n    \"b\":msg.payload.seg[0].col[2][2],\n    \"a\":255\n};\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 380,
        "y": 240,
        "wires": [
            [
                "7268712f3b07d692",
                "a72b4716853fe44e"
            ]
        ]
    },
    {
        "id": "7268712f3b07d692",
        "type": "ui_colour_picker",
        "z": "20061a0525813035",
        "name": "",
        "label": "Tertiary Color",
        "group": "5972d9ad77220186",
        "format": "rgb",
        "outformat": "object",
        "showSwatch": true,
        "showPicker": false,
        "showValue": false,
        "showHue": false,
        "showAlpha": false,
        "showLightness": true,
        "square": "false",
        "dynOutput": "false",
        "order": 3,
        "width": "4",
        "height": "1",
        "passthru": false,
        "topic": "",
        "topicType": "str",
        "className": "",
        "x": 810,
        "y": 240,
        "wires": [
            [
                "3a0342578562a1bb"
            ]
        ]
    },
    {
        "id": "3a0342578562a1bb",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Color 3",
        "func": "var color = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"col\": [\n    [],\n    [],\n    [color.r,color.g,color.b]\n    ]};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1030,
        "y": 240,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "01ec37e1d6dbdbcf",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Store WLED State",
        "func": "flow.set('wled_state', msg.payload);\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 390,
        "y": 520,
        "wires": [
            [
                "6d9cce310505691b"
            ]
        ]
    },
    {
        "id": "6d9cce310505691b",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 500,
        "wires": []
    },
    {
        "id": "0b9f9473c28ea35b",
        "type": "link out",
        "z": "20061a0525813035",
        "name": "WLED Status Trigger",
        "links": [
            "495852008b10fa64"
        ],
        "x": 1235,
        "y": 420,
        "wires": []
    },
    {
        "id": "495852008b10fa64",
        "type": "link in",
        "z": "20061a0525813035",
        "name": "WLED Status Trigger out",
        "links": [
            "0b9f9473c28ea35b"
        ],
        "x": 175,
        "y": 1020,
        "wires": [
            [
                "aba1b8a81745c9d8"
            ]
        ]
    },
    {
        "id": "6cf1b294fcb3d50f",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Palette",
        "func": "var palette = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"pal\": palette};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1030,
        "y": 320,
        "wires": [
            [
                "c49c2e97545f3c6d"
            ]
        ]
    },
    {
        "id": "99b50a94ffb7d037",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Effect",
        "func": "var effect = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"fx\": effect};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1020,
        "y": 280,
        "wires": [
            [
                "c49c2e97545f3c6d"
            ]
        ]
    },
    {
        "id": "e15cf5ebaf51a2d4",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set FX Speed",
        "func": "var speed = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"sx\": speed};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1040,
        "y": 360,
        "wires": [
            [
                "c49c2e97545f3c6d"
            ]
        ]
    },
    {
        "id": "c5e7bb6cea6bdcf6",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set FX Intensity",
        "func": "var ix = msg.payload;\nvar command = {\"seg\": []};\ncommand.seg[0]={\"ix\": ix};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1040,
        "y": 400,
        "wires": [
            [
                "c49c2e97545f3c6d"
            ]
        ]
    },
    {
        "id": "a64d4c43d1abbd1c",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Brightness",
        "func": "var bri = msg.payload;\nvar command = {\"bri\": bri};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1040,
        "y": 440,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "08f3c178fef1717c",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set Power",
        "func": "var pwr = msg.payload;\nvar command = {\"on\": pwr};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1030,
        "y": 480,
        "wires": [
            [
                "c49c2e97545f3c6d"
            ]
        ]
    },
    {
        "id": "33f86877297054b1",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Sync RX State",
        "func": "msg.payload = msg.payload.udpn.recv;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 400,
        "y": 560,
        "wires": [
            [
                "3b0c924df0265aa0",
                "d98bfc67f180eef3"
            ]
        ]
    },
    {
        "id": "3b0c924df0265aa0",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 610,
        "y": 540,
        "wires": []
    },
    {
        "id": "d98bfc67f180eef3",
        "type": "ui_switch",
        "z": "20061a0525813035",
        "name": "",
        "label": "RX Sync",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 6,
        "width": "3",
        "height": "1",
        "passthru": false,
        "decouple": "true",
        "topic": "",
        "topicType": "str",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "animate": true,
        "className": "",
        "x": 801,
        "y": 560,
        "wires": [
            [
                "a5a8d47e0628b923"
            ]
        ]
    },
    {
        "id": "a5a8d47e0628b923",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set RX Sync",
        "func": "var sync_rx = msg.payload;\nvar command = {\"udpn\": []};\ncommand.udpn = {\"recv\": sync_rx};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1030,
        "y": 560,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "bd25dff0adb01796",
        "type": "comment",
        "z": "20061a0525813035",
        "name": "Dusk/Dawn and On/Off Schedule",
        "info": "",
        "x": 770,
        "y": 700,
        "wires": []
    },
    {
        "id": "436d75b9f27e5f76",
        "type": "comment",
        "z": "20061a0525813035",
        "name": "Latest state in flow.get('wled_state')",
        "info": "",
        "x": 880,
        "y": 520,
        "wires": []
    },
    {
        "id": "609b51f90aa76770",
        "type": "bigtimer",
        "z": "20061a0525813035",
        "outtopic": "",
        "outpayload1": "55",
        "outpayload2": "128",
        "name": "Lightchanger",
        "comment": "Brighter at Dawn, Darker at Dusk",
        "lat": "37.09024",
        "lon": "-95.71289",
        "starttime": 5001,
        "endtime": "5000",
        "starttime2": 0,
        "endtime2": 0,
        "startoff": 0,
        "endoff": "60",
        "startoff2": 0,
        "endoff2": 0,
        "offs": 0,
        "outtext1": "",
        "outtext2": "",
        "timeout": 1440,
        "sun": true,
        "mon": true,
        "tue": true,
        "wed": true,
        "thu": true,
        "fri": true,
        "sat": true,
        "jan": true,
        "feb": true,
        "mar": true,
        "apr": true,
        "may": true,
        "jun": true,
        "jul": true,
        "aug": true,
        "sep": true,
        "oct": true,
        "nov": true,
        "dec": true,
        "day1": 0,
        "month1": 0,
        "day2": 0,
        "month2": 0,
        "day3": 0,
        "month3": 0,
        "day4": 0,
        "month4": 0,
        "day5": 0,
        "month5": 0,
        "day6": 0,
        "month6": 0,
        "day7": "",
        "month7": "",
        "day8": "",
        "month8": "",
        "day9": "",
        "month9": "",
        "day10": "",
        "month10": "",
        "day11": "",
        "month11": "",
        "day12": "",
        "month12": "",
        "d1": 0,
        "w1": 0,
        "d2": 0,
        "w2": 0,
        "d3": 0,
        "w3": 0,
        "d4": 0,
        "w4": 0,
        "d5": 0,
        "w5": 0,
        "d6": 0,
        "w6": 0,
        "xday1": 0,
        "xmonth1": 0,
        "xday2": 0,
        "xmonth2": 0,
        "xday3": 0,
        "xmonth3": 0,
        "xday4": 0,
        "xmonth4": 0,
        "xday5": 0,
        "xmonth5": 0,
        "xday6": 0,
        "xmonth6": 0,
        "xday7": "",
        "xmonth7": "",
        "xday8": "",
        "xmonth8": "",
        "xday9": "",
        "xmonth9": "",
        "xday10": "",
        "xmonth10": "",
        "xday11": "",
        "xmonth11": "",
        "xday12": "",
        "xmonth12": "",
        "xd1": 0,
        "xw1": 0,
        "xd2": 0,
        "xw2": 0,
        "xd3": 0,
        "xw3": 0,
        "xd4": 0,
        "xw4": 0,
        "xd5": 0,
        "xw5": 0,
        "xd6": 0,
        "xw6": 0,
        "suspend": false,
        "random": false,
        "randon1": false,
        "randoff1": false,
        "randon2": false,
        "randoff2": false,
        "repeat": false,
        "atstart": false,
        "odd": false,
        "even": false,
        "x": 610,
        "y": 760,
        "wires": [
            [
                "443dec52c0dad343"
            ],
            [],
            []
        ]
    },
    {
        "id": "61a35cedfa74c2ca",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Sync TX State",
        "func": "msg.payload = msg.payload.udpn.send;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 400,
        "y": 600,
        "wires": [
            [
                "87ecdcfaa4b394eb"
            ]
        ]
    },
    {
        "id": "87ecdcfaa4b394eb",
        "type": "ui_switch",
        "z": "20061a0525813035",
        "name": "",
        "label": "TX Sync",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 7,
        "width": "3",
        "height": "1",
        "passthru": false,
        "decouple": "true",
        "topic": "",
        "topicType": "str",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "animate": true,
        "className": "",
        "x": 801,
        "y": 600,
        "wires": [
            [
                "6af3572c04623de8"
            ]
        ]
    },
    {
        "id": "6af3572c04623de8",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set TX Sync",
        "func": "var sync_tx = msg.payload;\nvar command = {\"udpn\": []};\ncommand.udpn = {\"send\": sync_tx};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1030,
        "y": 600,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "6ec2f8b1ee552ff2",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "x": 770,
        "y": 980,
        "wires": []
    },
    {
        "id": "160c3c1ed01aaa38",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "",
        "repeat": "60",
        "crontab": "",
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 350,
        "y": 1020,
        "wires": [
            [
                "50546cc83e36ac02"
            ]
        ]
    },
    {
        "id": "42d0c2b377121952",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "x": 550,
        "y": 860,
        "wires": []
    },
    {
        "id": "c4d18c22e523b7dd",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Extract Playlist Cycle",
        "func": "var pl_status = msg.payload.pl;\nif (pl_status<0) {\n    msg.payload=false;\n} else {\n    msg.payload=true;\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 400,
        "y": 640,
        "wires": [
            [
                "b9130ecf78402d87"
            ]
        ]
    },
    {
        "id": "b9130ecf78402d87",
        "type": "ui_switch",
        "z": "20061a0525813035",
        "name": "",
        "label": "Cycle",
        "tooltip": "",
        "group": "5972d9ad77220186",
        "order": 5,
        "width": "3",
        "height": "1",
        "passthru": false,
        "decouple": "true",
        "topic": "",
        "topicType": "str",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "animate": true,
        "className": "",
        "x": 791,
        "y": 640,
        "wires": [
            [
                "0139b0e6b2ad46e6"
            ]
        ]
    },
    {
        "id": "0139b0e6b2ad46e6",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Set PL Cycle",
        "func": "var cycle = msg.payload;\nif (cycle) {\n    cycle = 0;\n} else {\n    cycle = -1;\n}\nvar command = {\"pl\": cycle};\nmsg.payload = command;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1030,
        "y": 640,
        "wires": [
            [
                "c49c2e97545f3c6d",
                "0b9f9473c28ea35b"
            ]
        ]
    },
    {
        "id": "e9f4ed4d210c1c76",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 1030,
        "y": 740,
        "wires": []
    },
    {
        "id": "8d9362946334803a",
        "type": "comment",
        "z": "20061a0525813035",
        "name": "Grab JSON API Status",
        "info": "",
        "x": 200,
        "y": 880,
        "wires": []
    },
    {
        "id": "cad7528c957e21d2",
        "type": "change",
        "z": "20061a0525813035",
        "name": "Extract State",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.state",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 990,
        "y": 1120,
        "wires": [
            [
                "7ad3960f4ad68b90",
                "7173090fa6a31236"
            ]
        ]
    },
    {
        "id": "7ad3960f4ad68b90",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 1190,
        "y": 1080,
        "wires": []
    },
    {
        "id": "e4d1608fa626c686",
        "type": "change",
        "z": "20061a0525813035",
        "name": "Extract Palette List",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.palettes",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1010,
        "y": 1200,
        "wires": [
            [
                "3e726b85c077af3d"
            ]
        ]
    },
    {
        "id": "bf6019e885c22b0f",
        "type": "change",
        "z": "20061a0525813035",
        "name": "Extract Effect List",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.effects",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1010,
        "y": 1160,
        "wires": [
            [
                "ce571197b5360ce2"
            ]
        ]
    },
    {
        "id": "ce571197b5360ce2",
        "type": "link out",
        "z": "20061a0525813035",
        "name": "WLED JSON Effect Out",
        "links": [
            "972e3add9b675c70"
        ],
        "x": 1195,
        "y": 1160,
        "wires": []
    },
    {
        "id": "3e726b85c077af3d",
        "type": "link out",
        "z": "20061a0525813035",
        "name": "WLED JSON Palettes Out",
        "links": [
            "bca8d7dea83d0e64"
        ],
        "x": 1195,
        "y": 1200,
        "wires": []
    },
    {
        "id": "972e3add9b675c70",
        "type": "link in",
        "z": "20061a0525813035",
        "name": "WLED JSON Effects In",
        "links": [
            "ce571197b5360ce2"
        ],
        "x": 115,
        "y": 1260,
        "wires": [
            [
                "ba65ab55754e9b9d"
            ]
        ]
    },
    {
        "id": "bca8d7dea83d0e64",
        "type": "link in",
        "z": "20061a0525813035",
        "name": "WLED JSON Palettes In",
        "links": [
            "3e726b85c077af3d"
        ],
        "x": 115,
        "y": 1360,
        "wires": [
            [
                "facb73c1d2434db3"
            ]
        ]
    },
    {
        "id": "8cf1fbb4f0597fc2",
        "type": "comment",
        "z": "20061a0525813035",
        "name": "Config nodes hold IP address and MQTT topic",
        "info": "",
        "x": 400,
        "y": 40,
        "wires": []
    },
    {
        "id": "ba65ab55754e9b9d",
        "type": "delay",
        "z": "20061a0525813035",
        "name": "",
        "pauseType": "rate",
        "timeout": "5",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "5",
        "rateUnits": "minute",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": true,
        "outputs": 1,
        "x": 260,
        "y": 1260,
        "wires": [
            [
                "d9aeaae159f9b2a5",
                "e56ee39e01f0fc71",
                "739eabf79ebf3df6"
            ]
        ]
    },
    {
        "id": "facb73c1d2434db3",
        "type": "delay",
        "z": "20061a0525813035",
        "name": "",
        "pauseType": "rate",
        "timeout": "5",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "5",
        "rateUnits": "minute",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": true,
        "allowrate": false,
        "outputs": 1,
        "x": 260,
        "y": 1360,
        "wires": [
            [
                "18a7e131123ac5c3",
                "565015a46e76c9ce",
                "4bba294bdb4b6010"
            ]
        ]
    },
    {
        "id": "2be269b4b7161fd2",
        "type": "delay",
        "z": "20061a0525813035",
        "name": "",
        "pauseType": "rate",
        "timeout": "5",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "1",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "outputs": 1,
        "x": 610,
        "y": 920,
        "wires": [
            [
                "1f2d0f60ee5f4fa1"
            ]
        ]
    },
    {
        "id": "18425db197cb1e31",
        "type": "delay",
        "z": "20061a0525813035",
        "name": "",
        "pauseType": "rate",
        "timeout": "5",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "2",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": true,
        "outputs": 1,
        "x": 140,
        "y": 1120,
        "wires": [
            [
                "f5c1c87d49bd869a"
            ]
        ]
    },
    {
        "id": "8581ada3105309ff",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "1",
        "payloadType": "num",
        "x": 410,
        "y": 700,
        "wires": [
            [
                "609b51f90aa76770"
            ]
        ]
    },
    {
        "id": "42994238fb5866f7",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "0",
        "payloadType": "num",
        "x": 410,
        "y": 740,
        "wires": [
            [
                "609b51f90aa76770"
            ]
        ]
    },
    {
        "id": "9d14b961e94629a4",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "manual",
        "payloadType": "str",
        "x": 410,
        "y": 780,
        "wires": [
            [
                "609b51f90aa76770"
            ]
        ]
    },
    {
        "id": "ef41f4cec9de1f60",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "auto",
        "payloadType": "str",
        "x": 410,
        "y": 820,
        "wires": [
            [
                "609b51f90aa76770"
            ]
        ]
    },
    {
        "id": "443dec52c0dad343",
        "type": "function",
        "z": "20061a0525813035",
        "name": "Clean up",
        "func": "var payload = parseInt(msg.payload);\nmsg = {};\nmsg.payload = payload;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 840,
        "y": 740,
        "wires": [
            [
                "e9f4ed4d210c1c76",
                "a64d4c43d1abbd1c"
            ]
        ]
    },
    {
        "id": "6f5960a0d23f18c2",
        "type": "trigger",
        "z": "20061a0525813035",
        "name": "",
        "op1": "",
        "op2": "",
        "op1type": "pay",
        "op2type": "nul",
        "duration": "1",
        "extend": false,
        "units": "ms",
        "reset": "",
        "bytopic": "all",
        "outputs": 1,
        "x": 110,
        "y": 220,
        "wires": [
            [
                "035c0a95c6788b1b",
                "57048ce993979ff9",
                "69a3d5ceff8c4e5c",
                "ed5f75ddba646f65",
                "ad7776af1e3e69e8",
                "ca5855770d303367",
                "be1cbbb9fa4120c4",
                "d93964e1a51f8aef",
                "d1134e8162368efa",
                "01ec37e1d6dbdbcf",
                "33f86877297054b1",
                "61a35cedfa74c2ca",
                "c4d18c22e523b7dd"
            ]
        ]
    },
    {
        "id": "aba1b8a81745c9d8",
        "type": "delay",
        "z": "20061a0525813035",
        "name": "",
        "pauseType": "rate",
        "timeout": "5",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "2",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": true,
        "outputs": 1,
        "x": 340,
        "y": 980,
        "wires": [
            [
                "50546cc83e36ac02"
            ]
        ]
    },
    {
        "id": "4a459a1fa08f07ac",
        "type": "switch",
        "z": "20061a0525813035",
        "name": "Pass if not null",
        "property": "payload",
        "propertyType": "msg",
        "rules": [
            {
                "t": "nnull"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 1,
        "x": 720,
        "y": 1120,
        "wires": [
            [
                "7023332786ef9284",
                "cad7528c957e21d2",
                "bf6019e885c22b0f",
                "e4d1608fa626c686"
            ]
        ]
    },
    {
        "id": "01b2f8038146ec9e",
        "type": "switch",
        "z": "20061a0525813035",
        "name": "Check success",
        "property": "statusCode",
        "propertyType": "msg",
        "rules": [
            {
                "t": "eq",
                "v": "200",
                "vt": "num"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 1,
        "x": 520,
        "y": 1120,
        "wires": [
            [
                "4a459a1fa08f07ac"
            ]
        ]
    },
    {
        "id": "10c1d182d82149a8",
        "type": "change",
        "z": "20061a0525813035",
        "name": "Gravicenter SOUND FX ON",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "132",
                "tot": "num"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1580,
        "y": 1260,
        "wires": [
            [
                "99b50a94ffb7d037"
            ]
        ]
    },
    {
        "id": "ccc7d28f2713bc68",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "FX On",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "true",
        "payloadType": "bool",
        "x": 1270,
        "y": 1420,
        "wires": [
            [
                "10c1d182d82149a8"
            ]
        ]
    },
    {
        "id": "ccae4bb59344aee2",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "FX Off",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "false",
        "payloadType": "bool",
        "x": 1270,
        "y": 1460,
        "wires": [
            [
                "ecca3e3a49ba7c8f"
            ]
        ]
    },
    {
        "id": "ecca3e3a49ba7c8f",
        "type": "change",
        "z": "20061a0525813035",
        "name": "SOLID",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "0",
                "tot": "num"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1470,
        "y": 1320,
        "wires": [
            [
                "99b50a94ffb7d037"
            ]
        ]
    },
    {
        "id": "18aef7d0388e4616",
        "type": "comment",
        "z": "20061a0525813035",
        "name": "HOMEKIT FLOW 4 LIGHTBULB",
        "info": "",
        "x": 1070,
        "y": 1240,
        "wires": []
    },
    {
        "id": "7509f965.646da8",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "On",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "true",
        "payload": "{\"On\":true}",
        "payloadType": "json",
        "x": 770,
        "y": 1460,
        "wires": [
            [
                "84c5345e.cea678"
            ]
        ]
    },
    {
        "id": "83aa9e6a.6ac9e",
        "type": "debug",
        "z": "20061a0525813035",
        "name": "HomeKit Out",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": true,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "payload",
        "statusType": "auto",
        "x": 1710,
        "y": 800,
        "wires": []
    },
    {
        "id": "6f909132.f78a",
        "type": "inject",
        "z": "20061a0525813035",
        "name": "Off",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "false",
        "payload": "{\"On\":false}",
        "payloadType": "json",
        "x": 770,
        "y": 1500,
        "wires": [
            [
                "84c5345e.cea678"
            ]
        ]
    },
    {
        "id": "84c5345e.cea678",
        "type": "homekit-service",
        "z": "20061a0525813035",
        "isParent": false,
        "hostType": "0",
        "bridge": "51de116c.bb01",
        "accessoryId": "",
        "parentService": "da94f3c27a89044a",
        "name": "FX Schalter ",
        "serviceName": "Switch",
        "topic": "",
        "filter": false,
        "manufacturer": "v0r73x",
        "model": "Default Model",
        "serialNo": "1.1.1",
        "firmwareRev": "1.1.1",
        "hardwareRev": "1.1.1",
        "softwareRev": "1.0.0",
        "cameraConfigVideoProcessor": "ffmpeg",
        "cameraConfigSource": "",
        "cameraConfigStillImageSource": "",
        "cameraConfigMaxStreams": 2,
        "cameraConfigMaxWidth": 1280,
        "cameraConfigMaxHeight": 720,
        "cameraConfigMaxFPS": 10,
        "cameraConfigMaxBitrate": 300,
        "cameraConfigVideoCodec": "libx264",
        "cameraConfigAudioCodec": "libfdk_aac",
        "cameraConfigAudio": false,
        "cameraConfigPacketSize": 1316,
        "cameraConfigVerticalFlip": false,
        "cameraConfigHorizontalFlip": false,
        "cameraConfigMapVideo": "0:0",
        "cameraConfigMapAudio": "0:1",
        "cameraConfigVideoFilter": "scale=1280:720",
        "cameraConfigAdditionalCommandLine": "-tune zerolatency",
        "cameraConfigDebug": false,
        "cameraConfigSnapshotOutput": "disabled",
        "cameraConfigInterfaceName": "",
        "characteristicProperties": "{}",
        "waitForSetupMsg": false,
        "outputs": 2,
        "x": 890,
        "y": 1320,
        "wires": [
            [],
            [
                "36b517a348cedf2b"
            ]
        ]
    },
    {
        "id": "36b517a348cedf2b",
        "type": "switch",
        "z": "20061a0525813035",
        "name": "extract boolean from payload",
        "property": "payload.On",
        "propertyType": "msg",
        "rules": [
            {
                "t": "true"
            },
            {
                "t": "false"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 1170,
        "y": 1320,
        "wires": [
            [
                "10c1d182d82149a8"
            ],
            [
                "ecca3e3a49ba7c8f"
            ]
        ]
    },
    {
        "id": "da94f3c27a89044a",
        "type": "homekit-service",
        "z": "20061a0525813035",
        "isParent": true,
        "hostType": "0",
        "bridge": "51de116c.bb01",
        "accessoryId": "",
        "parentService": "",
        "name": "OFFICE FX WLED",
        "serviceName": "Lightbulb",
        "topic": "",
        "filter": false,
        "manufacturer": "v0r73x",
        "model": "1.5.0",
        "serialNo": "Default Serial Number",
        "firmwareRev": "1.5.0",
        "hardwareRev": "1.5.0",
        "softwareRev": "1.5.0",
        "cameraConfigVideoProcessor": "ffmpeg",
        "cameraConfigSource": "",
        "cameraConfigStillImageSource": "",
        "cameraConfigMaxStreams": 2,
        "cameraConfigMaxWidth": 1280,
        "cameraConfigMaxHeight": 720,
        "cameraConfigMaxFPS": 10,
        "cameraConfigMaxBitrate": 300,
        "cameraConfigVideoCodec": "libx264",
        "cameraConfigAudioCodec": "libfdk_aac",
        "cameraConfigAudio": false,
        "cameraConfigPacketSize": 1316,
        "cameraConfigVerticalFlip": false,
        "cameraConfigHorizontalFlip": false,
        "cameraConfigMapVideo": "0:0",
        "cameraConfigMapAudio": "0:1",
        "cameraConfigVideoFilter": "scale=1280:720",
        "cameraConfigAdditionalCommandLine": "-tune zerolatency",
        "cameraConfigDebug": false,
        "cameraConfigSnapshotOutput": "disabled",
        "cameraConfigInterfaceName": "",
        "characteristicProperties": "{\"Brightness\":true,\"Hue\":true,\"Saturation\":true}",
        "waitForSetupMsg": false,
        "outputs": 2,
        "x": 910,
        "y": 1280,
        "wires": [
            [],
            [
                "28bf69c41a06db54"
            ]
        ]
    },
    {
        "id": "28bf69c41a06db54",
        "type": "homekit-rgb",
        "z": "20061a0525813035",
        "name": "",
        "x": 1110,
        "y": 1280,
        "wires": [
            [
                "e957543d68af7683"
            ]
        ]
    },
    {
        "id": "423d378c65f126c7",
        "type": "function",
        "z": "20061a0525813035",
        "name": "function 1",
        "func": "var mod = `{ \"r\": ${msg.payload.red}, \"g\": ${msg.payload.green}, \"b\": ${msg.payload.blue}, \"a\": 1 }`;\nmsg.payload = mod;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1600,
        "y": 1160,
        "wires": [
            [
                "8d827c8f67ed723d"
            ]
        ]
    },
    {
        "id": "e957543d68af7683",
        "type": "color-convert",
        "z": "20061a0525813035",
        "input": "rgb",
        "output": "rgb",
        "outputType": "object",
        "scaleInput": false,
        "x": 1290,
        "y": 1280,
        "wires": [
            [
                "423d378c65f126c7"
            ]
        ]
    },
    {
        "id": "8d827c8f67ed723d",
        "type": "json",
        "z": "20061a0525813035",
        "name": "",
        "property": "payload",
        "action": "",
        "pretty": false,
        "x": 1730,
        "y": 1160,
        "wires": [
            [
                "35347868cafaece4"
            ]
        ]
    },
    {
        "id": "5972d9ad77220186",
        "type": "ui_group",
        "name": "Office.FX",
        "tab": "17fb5dcb.932bc2",
        "order": 7,
        "disp": true,
        "width": "6",
        "collapse": true,
        "className": ""
    },
    {
        "id": "51de116c.bb01",
        "type": "homekit-bridge",
        "bridgeName": "Example Bridge",
        "pinCode": "111-11-111",
        "port": "",
        "allowInsecureRequest": false,
        "manufacturer": "Default Manufacturer",
        "model": "Default Model",
        "serialNo": "Default Serial Number",
        "firmwareRev": "",
        "hardwareRev": "",
        "softwareRev": "",
        "customMdnsConfig": false,
        "mdnsMulticast": true,
        "mdnsInterface": "",
        "mdnsPort": "",
        "mdnsIp": "",
        "mdnsTtl": "",
        "mdnsLoopback": true,
        "mdnsReuseAddr": true,
        "allowMessagePassthrough": true
    },
    {
        "id": "17fb5dcb.932bc2",
        "type": "ui_tab",
        "name": "LightBox",
        "icon": "lightbulb_outline",
        "order": 2,
        "disabled": false,
        "hidden": false
    }
]
