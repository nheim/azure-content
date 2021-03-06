<properties linkid="develop-mobile-tutorials-get-started-with-data-android" urlDisplayName="Get Started with Data" pageTitle="Get started with data (Android) - Windows Azure Mobile Services" writer="glenga"  metaKeywords="Windows Azure Android data, Azure mobile services data, " metaDescription="Learn how to store and access data from your Windows Azure Mobile Services Android app." metaCanonical="" disqusComments="1" umbracoNaviHide="1" />



# Get started with data in Mobile Services
<div class="dev-center-tutorial-selector sublanding">    
	<a href="/en-us/develop/mobile/tutorials/get-started-with-data-dotnet" title="Windows Store C#">Windows Store C#</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-js" title="Windows Store JavaScript">Windows Store JavaScript</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-wp8" title="Windows Phone">Windows Phone</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-ios" title="iOS">iOS</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-android" title="Android" class="current">Android</a><a href="/en-us/develop/mobile/tutorials/get-started-with-data-html" title="HTML">HTML</a> 
</div>	


<div class="dev-onpage-video-clear clearfix">
<div class="dev-onpage-left-content">

<p>This topic shows you how to use Windows Azure Mobile Services to leverage data in an Android app. In this tutorial, you will download an app that stores data in memory, create a new mobile service, integrate the mobile service with the app, and then login to the Windows Azure Management Portal to view changes to data made when running the app.</p>

</div>
<div class="dev-onpage-video-wrapper"><a href="http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Android-Getting-Started-With-Data-Connecting-your-app-to-Windows-Azure-Mobile-Services" target="_blank" class="label">watch the tutorial</a> <a style="background-image: url('/media/devcenter/mobile/videos/mobile-android-get-started-data-180x120.png') !important;" href="http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Android-Getting-Started-With-Data-Connecting-your-app-to-Windows-Azure-Mobile-Services" target="_blank" class="dev-onpage-video"><span class="icon">Play Video</span></a><span class="time">15:32</span></div>
</div>

<div class="dev-callout"><b>Note</b>
<p>This tutorial is intended to help you better understand how Mobile Services enables you to use Windows Azure to store and retrieve data from an Android app. As such, this topic walks you through many of the steps that are completed for you in the Mobile Services quickstart. If this is your first experience with Mobile Services, consider first completing the tutorial <a href="/en-us/develop/mobile/tutorials/get-started-android">Get started with Mobile Services</a>.</p>
</div>

This tutorial walks you through these basic steps:

1. [Download the Android app project] 
2. [Create the mobile service]
3. [Add a data table for storage]
4. [Update the app to use Mobile Services]
5. [Test the app against Mobile Services]

<div class="dev-callout"><strong>Note</strong> <p>To complete this tutorial, you need a Windows Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see <a href="http://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=AED8DE357" target="_blank">Windows Azure Free Trial</a>.</p></div> 

This tutorial requires the [Mobile Services Android SDK]; the <a href="https://go.microsoft.com/fwLink/p/?LinkID=280125" target="_blank">Android SDK</a>, which includes the Eclipse integrated development environment (IDE) and Android Developer Tools (ADT) plugin; and Android 4.2 or a later version. 

<div class="dev-callout"><b>Note</b>
<p>This tutorial provides instructions for installing both the Android SDK and the Mobile Services Android SDK. The downloaded GetStartedWithData project requires Android 4.2 or a later version. However, the Mobile Services SDK requires only Android 2.2 or a later version.</p>
</div>

<h2><a name="download-app"></a><span class="short-header">Download the project</span>Download the GetStartedWithData project</h2>

This tutorial is built on the [GetStartedWithData app][GitHub], which is an Android app. The UI for this app is identical to the app generated by the Mobile Services Android quickstart, except that added items are stored locally in memory. 

1. Download the `GetStartedWithData` sample app and expand the files on your computer. 

2. In Eclipse, click **File** then **Import**, expand **Android**, click **Existing Android Code into Workspace**, and then click **Next.** 

 ![][14]

3. Click **Browse**, browse to the location of the expanded project files, click **OK**, make sure that the TodoActivity project is checked, then click **Finish**. 

 ![][15]


	This imports the project files into the current workspace.
4. In Package Explorer, expand **GetStartedWithData**, **src**, and **.com.example.GetStartedWithData**, then examine the ToDoActivity.java file.

   ![][12]

   Notice that there are `//TODO` comments that specify the steps you must take to make this app work with your mobile service.

5. From the **Run** menu, click **Run As** and then click **1 Android Application** to start the project.

	<div class="dev-callout"><strong>Note</strong> <p>You can run this project using an Android phone, or using the Android emulator. Running with an Android phone  requires you to download a phone-specific USB driver.</p> <p>To run the project in the Android emulator, you must define a least one Android Virtual Device (AVD). Use the AVD Manager to create and manage these devices.</p></div>

6. In the app, type meaningful text, such as _Complete the tutorial_, and then click **Add**.

   ![][13]

   Notice that the saved text is stored in an in-memory collection and displayed in the list below.

<h2><a name="create-service"></a><span class="short-header">Create mobile service</span>Create a new mobile service in the Management Portal</h2>

<div chunk="../chunks/mobile-services-create-new-service-data.md" />

<h2><a name="add-table"></a><span class="short-header">Add a new table</span>Add a new table to the mobile service</h2>

<div chunk="../chunks/mobile-services-create-new-service-data-2.md" />

<h2><a name="update-app"></a><span class="short-header">Update the app</span>Update the app to use the mobile service for data access</h2>

Now that your mobile service is ready, you can update the app to store items in Mobile Services instead of the local collection. 

1. If you don't already have the [Mobile Services Android SDK], download it now and expand the compressed files.

2. Copy the `.jar` files from the SDK into the `libs` folder of the GetStartedWithData project.

3. In Package Explorer in Eclipse, right-click the `libs` folder, click **Refresh**, and the copied jar files will appear


  This adds the Mobile Services SDK reference to the workspace.

4. Open the AndroidManifest.xml file and add the following line:

		<uses-permission android:name="android.permission.INTERNET" />

  This enables the app to access Mobile Services in Windows Azure.

5. From Package Explorer, Open the TodoActivity.java file located in the com.example.getstartedwithdata package, and uncomment the following lines of code: 

		import com.microsoft.windowsazure.mobileservices.MobileServiceClient;
		import com.microsoft.windowsazure.mobileservices.MobileServiceTable;
		import com.microsoft.windowsazure.mobileservices.NextServiceFilterCallback;
		import com.microsoft.windowsazure.mobileservices.ServiceFilter;
		import com.microsoft.windowsazure.mobileservices.ServiceFilterRequest;
		import com.microsoft.windowsazure.mobileservices.ServiceFilterResponse;
		import com.microsoft.windowsazure.mobileservices.ServiceFilterResponseCallback;
		import com.microsoft.windowsazure.mobileservices.TableOperationCallback;
		import com.microsoft.windowsazure.mobileservices.TableQueryCallback;

		import java.net.MalformedURLException;
 
6. We will remove the in-memory list currently used by the app, so we can replace it with a mobile service. In the **ToDoActivity** class, comment out the following line of code, which defines the existing **toDoItemList** list.

		public List<ToDoItem> toDoItemList = new ArrayList<ToDoItem>();

7. Once the previous step is done, the project will indicate build errors. Search for the three remaining locations where the `toDoItemList` variable is used and comment out the sections indicated. Also remove `import java.util.ArrayList`. This fully removes the in-memory list. 

8. We now add our mobile service. Uncomment the following lines of code:

		private MobileServiceClient mClient;
		private private MobileServiceTable<ToDoItem> mToDoTable;

9. In the Management Portal, click **Mobile Services**, and then click the mobile service you just created.

10. Click the **Dashboard** tab and make a note of the **Site URL**, then click **Manage keys** and make a note of the **Application key**.

   ![][8]

  You will need these values when accessing the mobile service from your app code.

11. In the **onCreate** method, uncomment the following lines of code that define the **MobileServiceClient** variable:

		try {
		// Create the Mobile Service Client instance, using the provided
		// Mobile Service URL and key
			mClient = new MobileServiceClient(
					"MobileServiceUrl",
					"AppKey", 
					this).withFilter(new ProgressFilter());

			// Get the Mobile Service Table instance to use
			mToDoTable = mClient.getTable(ToDoItem.class);
		} catch (MalformedURLException e) {
			createAndShowDialog(new Exception("There was an error creating the Mobile Service. Verify the URL"), "Error");
		}

  This creates a new instance of MobileServiceClient that is used to access your mobile service. It also creates the MobileServiceTable instance that is used to proxy data storage in the mobile service.

12. In the code above, replace `MobileServiceUrl` and `AppKey` with the URL and application key from your mobile service, in that order.

13. Find the ProgressFilter class at the bottom of the file and uncomment it. This class displays a 'loading' indicator while MobileServiceClient is running network operations.

14. Uncommment these lines of the **checkItem** method:

		mToDoTable.update(item, new TableOperationCallback<ToDoItem>() {	
			public void onCompleted(ToDoItem entity, Exception exception,
					ServiceFilterResponse response) {
				if(exception == null){
					if (entity.isComplete()) {
						mAdapter.remove(entity);
					}
				} else {
					createAndShowDialog(exception, "Error");	
				}
			}
		});

   This sends an item update to the mobile service and removes checked items from the adapter.
    
15. Uncommment these lines of the **addItem** method:
	
		mToDoTable.insert(item, new TableOperationCallback<ToDoItem>() {
			
			public void onCompleted(ToDoItem entity, Exception exception,
					ServiceFilterResponse response) {
				if(exception == null){
					if (!entity.isComplete()) {
						mAdapter.add(entity);
					}
				} else {
					createAndShowDialog(exception, "Error");
				}				
			}
		});
		

  This code creates a new item and inserts it into the table in the remote mobile service.

16. Uncommment these lines of the **refreshItemsFromTable** method:

		mToDoTable.where().field("complete").eq(false)
		.execute(new TableQueryCallback<ToDoItem>() {
		     public void onCompleted(List<ToDoItem> result, 
		    		 int count, Exception exception, 
		    		 ServiceFilterResponse response) {
						
						if(exception == null){
							mAdapter.clear();
	
							for (ToDoItem item : result) {
								mAdapter.add(item);
							}
						} else {
							createAndShowDialog(exception, "Error");
						}
					}
				}); 

	This queries the mobile service and returns all items that are not marked as complete. Items are added to the adapter for binding.
		

Now that the app has been updated to use Mobile Services for backend storage, it's time to test the app against Mobile Services.

<h2><a name="test-app"></a><span class="short-header">Test the app</span>Test the app against your new mobile service</h2>

1. From the **Run** menu, click **Run** to start the project in the Android emulator.

	This executes your app, built with the Android SDK, that uses the client library to send a query that returns items from your mobile service.

5. As before, type meaningful text, then click **Add**.

   This sends a new item as an insert to the mobile service.

3. In the [Management Portal], click **Mobile Services**, and then click your mobile service.

4. Click the **Data** tab, then click **Browse**.

   ![][9]
  
   Notice that the **TodoItem** table now contains data, with id values generated by Mobile Services, and that columns have been automatically added to the table to match the TodoItem class in the app.

This concludes the **Get started with data** tutorial for Android.

## <a name="next-steps"> </a>Next steps

This tutorial demonstrated the basics of enabling an Android app to work with data in Mobile Services. 

Next, consider completing one of the following tutorials that is based on the GetStartedWithData app that you created in this tutorial:

* [Validate and modify data with scripts]
  <br/>Learn more about using server scripts in Mobile Services to validate and change data sent from your app.

* [Refine queries with paging]
  <br/>Learn how to use paging in queries to control the amount of data handled in a single request.

Once you have completed the data series, try these other Android tutorials:

* [Get started with authentication] 
	<br/>Learn how to authenticate users of your app.

* [Get started with push notifications] 
  <br/>Learn how to send a very basic push notification to your app with Mobile Services.

<!-- Anchors. -->
[Download the Android app project]: #download-app
[Create the mobile service]: #create-service
[Add a data table for storage]: #add-table
[Update the app to use Mobile Services]: #update-app
[Test the app against Mobile Services]: #test-app
[Next Steps]:#next-steps

<!-- Images. -->
[0]: ../Media/mobile-quickstart-startup-android.png
[1]: ../../Shared/Media/plus-new.png
[2]: ../Media/mobile-create.png
[3]: ../Media/mobile-create-page1.png
[4]: ../Media/mobile-create-page2.png
[5]: ../Media/mobile-data-tab-empty.png
[6]: ../Media/mobile-create-todoitem-table.png
[7]: ../Media/mobile-add-reference-android.png
[8]: ../Media/mobile-dashboard-tab.png
[9]: ../Media/mobile-todoitem-data-browse.png
[10]: ../Media/mobile-data-sample-download-android.png
[11]: ../Media/mobile-add-android-properties.png
[12]: ../Media/mobile-eclipse-project.png
[13]: ../Media/mobile-quickstart-startup-android.png
[14]: ../Media/mobile-services-import-android-workspace.png
[15]: ../Media/mobile-services-import-android-project.png


<!-- URLs. -->
[Validate and modify data with scripts]: ./mobile-services-validate-and-modify-data-dotnet.md
[Refine queries with paging]: ./mobile-services-paging-data-android.md
[Get started with Mobile Services]: ./mobile-services-get-started-android.md
[Get started with data]: ./mobile-services-get-started-with-data-android.md
[Get started with authentication]: ./mobile-services-get-started-with-users-android.md
[Get started with push notifications]: ./mobile-services-get-started-with-push-android.md
[WindowsAzure.com]: http://www.windowsazure.com/
[Windows Azure Management Portal]: https://manage.windowsazure.com/
[Management Portal]: https://manage.windowsazure.com/
[Mobile Services Android SDK]: http://go.microsoft.com/fwlink/p/?LinkID=280126
[GitHub]:  http://go.microsoft.com/fwlink/p/?LinkID=282122
[Android SDK]: https://go.microsoft.com/fwLink/p/?LinkID=280125
