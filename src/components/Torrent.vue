<template>
<v-card ripple
                    flat  class="pointer torrent"
                     :class="
                        containsTorrent(torrent.hash) ? 'torrent_selected' : ''
                    "
                    @click.native="selectTorrent(torrent.hash)">
    <v-layout row wrap :class="`pa-4 ml-0 project ${torrent.state}`">
                        <v-flex xs12 sm2 md3>
                            <div class="caption grey--text">Torrent title</div>
                            <div>{{ torrent.name }}</div>
                        </v-flex>
                        <v-flex xs6 sm1 md1 class="mr-2">
                            <div class="caption grey--text">Size</div>
                            <div>
                                {{
                                    torrent.size.substring(
                                        0,
                                        torrent.size.indexOf(' ')
                                    )
                                }}
                                <span class="caption grey--text">{{
                                    torrent.size.substring(
                                        torrent.size.indexOf(' ')
                                    )
                                }}</span>
                            </div>
                        </v-flex>
                        <v-flex xs5 sm1 md1 class="mr-2">
                            <div class="caption grey--text">Done</div>
                            <div>
                                {{
                                    torrent.dloaded.substring(
                                        0,
                                        torrent.dloaded.indexOf(' ')
                                    )
                                }}
                                <span class="caption grey--text">{{
                                    torrent.dloaded.substring(
                                        torrent.dloaded.indexOf(' ')
                                    )
                                }}</span>
                            </div>
                        </v-flex>
                        <v-flex xs6 sm1 md1 class="mr-2">
                            <div class="caption grey--text">Download</div>
                            <div>
                                {{
                                    torrent.dlspeed.substring(
                                        0,
                                        torrent.dlspeed.indexOf(' ')
                                    )
                                }}
                                <span class="caption grey--text">{{
                                    torrent.dlspeed.substring(
                                        torrent.dlspeed.indexOf(' ')
                                    )
                                }}</span>
                            </div>
                        </v-flex>
                        <v-flex xs5 sm1 md1 class="mr-2">
                            <div class="caption grey--text">Upload</div>
                            <div>
                                {{
                                    torrent.upspeed.substring(
                                        0,
                                        torrent.upspeed.indexOf(' ')
                                    )
                                }}
                                <span class="caption grey--text">{{
                                    torrent.upspeed.substring(
                                        torrent.upspeed.indexOf(' ')
                                    )
                                }}</span>
                            </div>
                        </v-flex>
                        <v-flex xs6 sm1 md1 class="mr-2">
                            <div class="caption grey--text">ETA</div>
                            <div>{{ torrent.eta }}</div>
                        </v-flex>
                        <v-flex xs5 sm1 md1 class="mr-2">
                            <div class="caption grey--text">Peers</div>
                            <div>
                                {{ torrent.num_leechs }}
                                <span class="grey--text caption"
                                    >/{{ torrent.available_peers }}</span
                                >
                            </div>
                        </v-flex>
                        <v-flex xs5 sm1 md1 class="mr-2">
                            <div class="caption grey--text">Seeds</div>
                            <div>
                                {{ torrent.num_seeds }}
                                <span class="grey--text caption"
                                    >/{{ torrent.available_seeds }}</span
                                >
                            </div>
                        </v-flex>
                        <v-flex xs4 sm12 md1>
                            <div class="right">
                                <v-chip
                                    small
                                    :class="
                                        `${torrent.state} white--text my-2 caption`
                                    "
                                    >{{ torrent.state }}</v-chip
                                >
                            </div>
                        </v-flex>
                        <v-flex xs12 sm12 md12>
                            <v-progress-linear
                                height="3"
                                color="cyan darken-1"
                                background-color="cyan lighten-3"
                                :value="(torrent.dloaded / torrent.size) * 100"
                            ></v-progress-linear>
                        </v-flex>
                    </v-layout>
                      <v-divider></v-divider>
                </v-card>
</template>

<script>
export default {
    name:'Torrent',
    props: {
        torrent: Object
    },
    methods: {selectTorrent(hash) {
           if (this.containsTorrent(hash)) {
        this.$store.commit('SET_SELECTED', {type:"remove", hash})
      } else {
        this.$store.commit('SET_SELECTED', {type:"add", hash})
      }
        },
        containsTorrent(hash) {
            return this.$store.getters.containsTorrent(hash)
        },}
}
</script>

<style>
.project.done {
    border-left: 4px solid #3cd1c2;
}
.project.busy {
    border-left: 4px solid #ffaa2c;
}
.project.fail {
    border-left: 4px solid #f83e70;
}
.project.paused {
    border-left: 4px solid #cfd8dc;
}
.v-chip.done {
    background: #3cd1c2 !important;
}
.v-chip.busy {
    background: #ffaa2c !important;
}
.v-chip.fail {
    background: #f83e70 !important;
}
.v-chip.paused {
    background: #cfd8dc !important;
}

.pointer {
    cursor: pointer;
}
</style>