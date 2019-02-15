<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="videos"></VideoList>
    
  </div>

</template>

<script>
import axios from 'axios';
import VideoList from './components/VideoList'
import SearchBar from './components/SearchBar';
const API_KEY=`AIzaSyCEXyZdll0lkbLHyUrpVZCVUnUY1MDjfXg`;

export default {
  name:"App",
  components:{
    SearchBar,
    VideoList
  },
  data:function(){
    return { videos: [] };
  },
  methods:{
    onTermChange(searchTerm){
      console.log(searchTerm)
      axios.get('https://www.googleapis.com/youtube/v3/search',{params:{
        key:API_KEY,
        type:'video',
        part:'snippet',
        q:searchTerm
      }})
      .then(response=>{
        this.videos=response.data.items
      })
    }
  }
};
</script>
