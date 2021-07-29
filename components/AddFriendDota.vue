<template>
    <div>
        <b-button v-b-modal.addFriendDota variant="primary">Add Friend</b-button>

        <b-modal id="addFriendDota" title="Friend" ok-title="Save" @ok="onSubmit">
            <form action="#">

                <b-form-group
                    label="User ID"
                    label-for="user_id">
                    
                    <b-form-input id="user_id" v-model="friend.user_id" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="User Name"
                    label-for="user_name">
                    
                    <b-form-input id="user_name" v-model="friend.user_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Player Name"
                    label-for="Player_name">
                    
                    <b-form-input id="player_name" v-model="friend.player_name" trim></b-form-input>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            friend: {}
        }
    },
    methods:{
        async onSubmit(){
            this.$axios.post('/api/friends/', this.friend)
            .then((res)=>{
                if(res.status==202){
                    alert('Successfully added a friend')
                    this.$emit('onAdd')
                }
            })
        }
    }
    
}
</script>