<script>
import axios from "axios";
export default {
  data: function () {
    return {};
  },
  created: function () {
    delete axios.defaults.headers.common["Authorization"];
    localStorage.removeItem("jwt");
    localStorage.setItem("flashMessage", "Logged Out!");
    this.$router.push("/");
  },
};
</script>
