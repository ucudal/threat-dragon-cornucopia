<template>
<b-card class="threat-card">
        <b-card-text>
            <b-row>
                <b-col>
                    <a href="javascript:void(0)" @click="threatSelected()" v-if="!!number">#{{ number }} {{ title || 'Unknown Threat' }}</a>
                    <a href="javascript:void(0)" @click="threatSelected()" v-else>{{ title || 'Unknown Threat' }}</a>
                </b-col>
            </b-row>
            <b-row v-if="modelType !== 'EOP' && type">
                <b-col>
                    {{ type }}
                </b-col>
            </b-row>
            <b-row v-if="modelType === 'EOP'">
                <b-col>
                    <b-row>
                        <b-col>
                            {{ cardsuit }}
                        </b-col>
                    </b-row>
                    <b-row>
                        <b-col>
                            {{ cardnumber }}
                        </b-col>
                    </b-row>
                </b-col>
            </b-row>
            <b-row>
                <b-col>
                    <font-awesome-icon 
                        icon="check"
                        class="threat-icon gray-icon"
                        :title="status"
                        v-if="status === 'NotApplicable'" />
                    <font-awesome-icon 
                        icon="check"
                        class="threat-icon green-icon"
                        :title="status"
                        v-if="status === 'Mitigated'" />
                    <font-awesome-icon 
                        icon="exclamation-triangle"
                        class="threat-icon red-icon"
                        :title="status"
                        v-if="status === 'Open'" />

                    <font-awesome-icon
                        icon="circle"
                        class="threat-icon darkred-icon"
                        :title="severity"
                        v-if="severity === 'Critical'" />
                    <font-awesome-icon 
                        icon="circle"
                        class="threat-icon red-icon"
                        :title="severity"
                        v-if="severity === 'High'" />
                    <font-awesome-icon 
                        icon="circle"
                        class="threat-icon orange-icon"
                        :title="severity"
                        v-if="severity === 'Medium'" />
                    <font-awesome-icon 
                        icon="circle"
                        class="threat-icon yellow-icon"
                        :title="severity"
                        v-if="severity === 'Low'" />
                    <font-awesome-icon 
                        icon="circle"
                        class="threat-icon gray-icon"
                        :title="severity"
                        v-if="severity === 'TBD'" />
                </b-col>
                <b-col align-h="end">
                    <b-badge :v-if="!!modelType">{{ modelType }}</b-badge>
                </b-col>
            </b-row>
        </b-card-text>
    </b-card>
</template>

<style lang="scss" scoped>
.threat-card {
    font-size: 14px;
}

.threat-title {
    margin-bottom: 5px;
}

.threat-icon {
    margin: 2px;
}

.green-icon {
    color: $green;
}

.darkred-icon {
    color: $firebrick;
}

.red-icon {
    color: $red;
}

.orange-icon {
    color: $darkorange;
}

.yellow-icon {
    color: $yellow;
}

.gray-icon {
    color: $gray;
}

</style>

<script>
export default {
    name: 'TdGraphThreats',
    props: {
        threat: {
            type: Object,
            required: true
        }
    },

    computed: {
        id() { return this.threat.id; },
        status() { return this.threat.status; },
        severity() { return this.threat.severity; },
        description() { return this.threat.description; },
        title() { return this.threat.title; },
        type() { return this.threat.type; },
        mitigation() { return this.threat.mitigation; },
        modelType() { return this.threat.modelType; },
        number() { return this.threat.number; },
        cardsuit() { return this.threat.cardSuit; },
        cardnumber() { return this.threat.cardNumber; }
    },

    methods: {
        threatSelected() {
            this.$emit('threatSelected', this.id,'old');
        }
    }
};

</script>