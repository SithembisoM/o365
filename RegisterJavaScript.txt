<script type="text/javascript" src="_layouts/15/sp.runtime.js"></script>
<script type="text/javascript" src="_layouts/15/sp.js"></script>
<script>
function AddCustomActions() {
try{
    var clientContext = new SP.ClientContext();
	var site = clientContext.get_web();
	var UserCustomActions = site.get_userCustomActions();
	
 newUserCustomAction = UserCustomActions.add();
    newUserCustomAction.set_location('ScriptLink');
    newUserCustomAction.set_scriptSrc('~SiteCollection/SiteAssets/alert.js');
    newUserCustomAction.set_sequence(10);
    newUserCustomAction.set_title('New Alert');
    newUserCustomAction.set_description('Global Alert');
    newUserCustomAction.update();
 
   clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceeded), Function.createDelegate(this, this.onQueryFailed));
   
	
   }catch(ex)
   {
   alert('Error: ' + ex);
   }
}
function onQuerySucceeded(sender, args) {
    alert('New Support files added to Site.\n\nRefresh the page.');
}
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + '\n' + args.get_stackTrace());
}

AddCustomActions()
</script>