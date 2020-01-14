<template>
    <div>
        <textarea v-model="msg" placeholder="enter getEntities json"></textarea>
        <p style="white-space: pre-line;">{{ warning }}</p>
        <code>
            <div v-for="(portal, idx) in portals" :key="idx">
                &lt;Placemark&gt;<br/>
                &lt;name&gt;{{portal.name}}&lt;/name&gt;<br/>
                &lt;Point&gt;&lt;coordinates&gt;{{portal.lon + ',' + portal.lat + ',0'}}&lt;/coordinates&gt;&lt;/Point&gt;<br/>
                &lt;styleUrl&gt;#pokestop&lt;/styleUrl&gt;<br/>
                &lt;/Placemark&gt;
            </div>
        </code>
    </div>
</template>

<script>
    export default {
        name: 'Portal',
        props: {
        },
        data() {
            return {
                portals: [],
                msg: '',
                warning: ''
            }
        },
        methods: {
            fetch() {
                let map = JSON.parse('[' + this.msg + ']')[0].result.map;

                Object.keys(map).forEach(i => {
                    if (typeof map[i].gameEntities !== 'undefined') {
                        for (let j in map[i].gameEntities) {
                            if (typeof map[i].gameEntities[j][2][8] !== 'undefined') {
                                let myObj = {
                                    name: map[i].gameEntities[j][2][8],
                                    lat: map[i].gameEntities[j][2][2].toString().slice(0, 2) + '.' + map[i].gameEntities[j][2][2].toString().slice(2),
                                    lon: map[i].gameEntities[j][2][3].toString().slice(0, 2) + '.' + map[i].gameEntities[j][2][3].toString().slice(2)
                                };
                                this.portals.push(myObj);
                            }
                        }
                    }
                });
            }
        },
        watch: {
            msg: function () {
                if (this.msg !== '') {
                    this.fetch();
                }
            }
        }
    }
</script>
