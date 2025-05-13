<script setup>
import { RouterLink, RouterView } from 'vue-router';
import { onMounted } from 'vue';
import axios from 'axios';

onMounted(async () =>{
    try {
        await axios.post('http://127.0.0.1:5000/blogs', {access_token: localStorage.getItem('access_token')});
    } catch(err) {
        const token = await axios.post('http://127.0.0.1:5000/refresh', {refresh_token: localStorage.getItem('refresh_token')});
        localStorage.setItem('access_token', token.data.access_token);
        localStorage.setItem('refresh_token', token.data.refresh_token);
    }
})
</script>

