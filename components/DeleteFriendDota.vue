<template>
    <div>

        <b-modal id="deleteFriendDota" title="Delete Friend" ok-title="Delete" @ok="onDelete" ok-variant="danger">
            Are You Sure about deleting this friend?<br><br>
            <h2>{{friend.user_id}}</h2> 
            <h5>- {{friend.player_name}}</h5>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        friend: {}
    },
    methods: {
        async onDelete(){
            this.$axios.delete('/api/friends/' + this.friend.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Friend is deleted successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>