<template>
    <div class="body">
        <NavBar/>
        <EditFriendDota :friend="selectedFriend"/>
        <DeleteFriendDota :friend="selectedFriend" @onDeleted="getAll"/>
        <div class="container"><br>
            <a href="/dashboard" class="btn btn-secondary btn-sm"> Back to Dashboard</a><br><br>
            <h1 style="color: black;">
                Friends
                <AddFriendDota class="float-right" @onAdd="getAll"/>
            </h1>
            

            <table class="table table-boredered tabled-striped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>User ID</th>
                        <th>Username</th>
                        <th>Player Name</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="info" v-for="friend in friends" :key="friend.id">
                        <td>{{friend.user_id}}</td>
                        <td>{{friend.user_name}}</td>
                        <td>{{friend.player_name}}</td>
                        <td>
                            <b-button @click="onEdit(friend)" variant="info" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(friend)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
   data(){
       return{
           friends:[],
           selectedFriend: {}
       }
   },
   methods:{
        async getAll(){
            await this.$axios.get('/api/friends')
            .then((res)=>{
                if(res.status==200) {
                    this.friends = res.data
                    console.log(this.friends)
                }
            })
        },
        onEdit(selectedFriend) {
            this.selectedFriend = selectedFriend;
            this.$bvModal.show('editFriendDota')
        },
        onDelete(selectedFriend) {
            this.selectedFriend = selectedFriend;
            this.$bvModal.show('deleteFriendDota')
        }
   },
   created(){
       this.getAll()
   }
}
</script>
