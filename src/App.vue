<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row" >
    <VideoDetail :video="selectedVideo" />
    <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
    </div>
  </div>

</template>

<script>
import axios from 'axios';
import VideoList from './components/VideoList'
import SearchBar from './components/SearchBar';
import VideoDetail from './components/VideoDetail'
const API_KEY=``;

export default {
  name:"App",
  components:{
    SearchBar,
    VideoList,
    VideoDetail
  },
  data:function(){
    return { videos: [], selectedVideo:null };
  },
  methods:{
    onVideoSelect(video){
      this.selectedVideo=video
    },
    onTermChange(searchTerm){
      // console.log(searchTerm)
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
