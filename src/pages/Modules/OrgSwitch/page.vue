<template>
    <div />
</template>
<script>
const app = require("@/config");
export default {
    mounted () {
        let positon = localStorage.getItem("role");
        if (positon === "指导老师") {
            this.$router.push({
                name: "OrgDetail",
                query: {
                    id: this.$route.query.overrideDptId || localStorage.getItem("defaultDepartId")
                }
            });
        } else if (positon === "管理员") {
            if (app.checkPermission("Organization.UnitAdminUser") || app.checkPermission("Organization.XSLHH") || app.checkPermission("Organization.TwAdminUser")) {
                this.$router.push({name: 'OrgList'});
            } else if (app.checkPermission("Organization.DepartAdminUser")) {
                this.$router.push({name: 'OrgDetail'});
            }
        } else {
            this.$router.push({name: 'OrgDetail'});
        }
    }
}
</script>
