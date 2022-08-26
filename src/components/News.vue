<template>
    <div class="News">
        <div>
            <h3>Nothing new yet</h3>
            <h4>Things will be updated later</h4>
            
        <a href="https://www.mvg.de/"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSD9iW2bmA5NsUwf7eZoyhJaQoQQBjiO4NsGg&usqp=CAU" alt="Ubahn" class="Tram"></a>
        </div>
    </div>
<br /><br />
    <h1>Aktuelle Abfahrten am Hauptbahnhof Karlsruhe</h1>
    <br />
    <div v-for="fahrt in abfahrten" class="entry">
        <div>
            <span>{{fahrt.name}}</span>
            <span>{{fahrt.uhrzeit}}</span>
            <span>Gleis: {{fahrt.gleis}}</span>
        </div>
        <div>
            {{fahrt.pfad}}
        </div>
    </div>
</template>


<script setup>
import { onMounted, ref } from 'vue';
const abfahrten = ref(null);

function xmlToJson(xml) {
	
	// Create the return object
	var obj = {};

	// console.log(xml.nodeType, xml.nodeName );
	
	if (xml.nodeType == 1) { // element
		// do attributes
		if (xml.attributes.length > 0) {
		obj["@attributes"] = {};
			for (var j = 0; j < xml.attributes.length; j++) {
				var attribute = xml.attributes.item(j);
				obj["@attributes"][attribute.nodeName] = attribute.nodeValue;
			}
		}
	} 
	else if (xml.nodeType == 4) { // cdata section
		obj = xml.nodeValue
	}

	// do children
	if (xml.hasChildNodes()) {
		for(var i = 0; i < xml.childNodes.length; i++) {
			var item = xml.childNodes.item(i);
			var nodeName = item.nodeName;
			if (typeof(obj[nodeName]) == "undefined") {
				obj[nodeName] = xmlToJson(item);
			} else {
				if (typeof(obj[nodeName].length) == "undefined") {
					var old = obj[nodeName];
					obj[nodeName] = [];
					obj[nodeName].push(old);
				}
				if (typeof(obj[nodeName]) === 'object') {
					obj[nodeName].push(xmlToJson(item));
				}
			}
		}
	}
	return obj;
};

onMounted(async () => {
    // https://api.deutschebahn.com/timetables/v1/plan/8000191/220825/16

    const currentDate = new Date().toISOString(); // 2022-08-26T08:16:31.462Z
    const date = currentDate.substr(2, 8).replaceAll("-", "");
    const hour = new Date().getHours();

    const response = await fetch("https://api.deutschebahn.com/timetables/v1/plan/8000191/"+date+"/"+ hour, {
        headers: {
            Authorization: "Bearer d8d1bfda2a81946a5b80eb94370b20fd"
        }
    })


    const json = xmlToJson(new window.DOMParser().parseFromString(await response.text(), "text/xml"));
    console.log(json.timetable.s);
    //console.log(await response.text());
    
    const entries = json.timetable.s;

    abfahrten.value = entries.filter(entry => !!entry.dp).map(entry => {
        console.log(entry.tl["@attributes"])
        const name = entry.tl["@attributes"].c == "S" ? "S" + entry.dp["@attributes"].l : entry.tl["@attributes"].c + entry.tl["@attributes"].n;
        const uhrzeit = entry.dp["@attributes"].pt.substr(6, 2) + ":" + entry.dp["@attributes"].pt.substr(8, 2)//entry.elements[1].attributes.pt.substr(6, 2) + ":" + entry.elements[1].attributes.pt.substr(8, 2);

        const stationen = entry.dp["@attributes"].ppth.split("|")
        const pfad = stationen[0] + " > " + stationen[stationen.length-1]
        const gleis = entry.dp["@attributes"].pp
        return {
            name,
            uhrzeit,
            pfad,
            gleis
        }
    }).sort((elememt1, elememt2) => {
        const h1 = Number.parseInt(elememt1.uhrzeit.split(":")[0])
        const h2 = Number.parseInt(elememt2.uhrzeit.split(":")[0])
        const m1 = Number.parseInt(elememt1.uhrzeit.split(":")[1])
        const m2 = Number.parseInt(elememt2.uhrzeit.split(":")[1])

        if(h1 < h2 || h1 == h2 && m1 < m2) {
            return -1
        }
    })

})
</script>

<style lang="scss">

.entry {
    display: flex;
    flex-direction: column;
    grid-template-columns: auto auto;
    padding: 5px;

    &:not(:last-of-type) {
        border-bottom: 1px solid gray;
    }

    > div:first-of-type {
        display: flex;
        gap: 5px;

        > span:first-of-type {
            font-size: 18px;
            font-weight: bold;
        }

        > span:nth-of-type(2) {
            color: red;
        }

        > span:last-of-type {
            margin-left: auto;
        }
    }
}

</style>


