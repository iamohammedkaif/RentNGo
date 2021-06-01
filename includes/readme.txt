left bar contents:

1.all users registered(amount due-fines)account is inactive or active?
2.all drivers registered with their vehicles
3.vehicle details-brand,fuel type,model, facilities....
4.booking status, confirmed/cancelled, paid or not paid, ride completed or on-going
5.manage pages-TnC, FAQs, privacy
6.customer care details- update

var user = firebase.auth().currentUser;

user.updateProfile({
  displayName: "Jane Q. User",
  photoURL: "https://example.com/jane-q-user/profile.jpg"
}).then(function() {
  // Update successful.
}).catch(function(error) {
  // An error happened.
});

var auth = firebase.auth();
var emailAddress = "user@example.com";

auth.sendPasswordResetEmail(emailAddress).then(function() {
  // Email sent.
}).catch(function(error) {
  // An error happened.
});

var user = firebase.auth().currentUser;

user.delete().then(function() {
  // User deleted.
}).catch(function(error) {
  // An error happened.
});

queries.Read(){
   document.write("<br><h3 align='center'>Manage Queries</h3><br>");
        document.write("<table border='2'>"+
                            "<thead align='center'>"+
                                "<td>UID</td>"+
                                "<td>Name</td>"+
                                "<td>Email</td>"+
                                "<td>Message</td>"+
                                "<td>Reply</td>"+
                                "<td>Status</td>"+
                                "<td>Action</td>"+
                            "</thead>"
                    );
        var path="queries";
        app_firebase.databaseApi.read(path,successFn,msgHandler);
        function successFn(snapShot){
            if(!! snapShot && !!snapShot.val()){
                var name="",email="",message="",status="",reply="";
                var data=snapShot.val();
                var keys=Object.keys(data);
                for(var i=0;i<keys.length;i++){
                    id=keys[i];
                    name=data[id].name;
                    email=data[id].email;
                    message=data[id].message;
                    status=data[id].status;
                    reply=data[id].reply;
                    console.log(id);
                    document.write("<tr align='center'>");
                    document.write("<td>"+id+"</td>");
                    document.write("<td>"+name+"</td>");
                    document.write("<td>"+email+"</td>");
                    document.write("<td>"+message+"</td>");
                    document.write("<td><input type='text' ondblclick='queries.fck()' onclick='queries.SetInputID(this)'/></td>");
                    document.write("<td>"+status+"</td>");
                    document.write("<td>"+
                                        "<div>"+
                                            "<button onclick='queries.Show()'>Update</button>"+
                                            "<button onclick='queries.SetDeleteID(this)' ondblclick='queries.Delete(this)'>Delete</button>"+
                                        "</div>"+
                                    "</td></tr>"
                                );
                   
                }
                document.write("</table>"); 
            }
            else
                console.log('No Data Found');
        }
}