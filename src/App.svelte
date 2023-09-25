<script>
	let selectedContact = null;
	let contacts = []; 
	let email;
	let fullName;
	let address;
	let phoneNumber;
	let date;
	let activeComponent="writeUp"
	let duplicateError = false;
	const displayInputFormPage = function(){
		activeComponent = 'inputFormPage'
	}
	const clearInputFormPage = function(){
		
		activeComponent = 'writeUp'
		fullName = email = address = phoneNumber = date =""
		duplicateError = false;
		selectedContact=null
	}
	const deleteContact = function(){
		const newContacts = contacts.filter((item)=>item !== selectedContact)
		contacts =[...newContacts]
		activeComponent = ''
	}
	const editContactInfo = function(){
		duplicateError = false;
		activeComponent = 'inputFormPage'
		fullName = selectedContact.fullName;
		email = selectedContact.email;
		address= selectedContact.address;
		phoneNumber = selectedContact.phoneNumber;
		date = selectedContact.date;
	}
	const createContact = function(){
		duplicateError = false;
	const contact = {email,address,phoneNumber,fullName,date}

	if(selectedContact){
		const data = contacts.filter((item) => item !== selectedContact)
		duplicateError=data.some((item)=>item.fullName===fullName)
		if(duplicateError)return
		contacts=data

	}
	
	if(fullName === ' ' || !fullName){
		return;
	}
	if(contacts.some((item)=> item.fullName === fullName)){
		duplicateError = true
		return;
	}


	contacts=[...contacts,contact]
	selectedContact=null
	}
	const displayContactInfo = function(contact){
		activeComponent ='contactInfoSection'
		selectedContact = contact
	}
</script>

<main class="main">
<div class = "leftSection">
	<div class = "contaxtsTitle"> 
	<div class = "contaxtsTitle">
		<h1 style="color: aliceblue; margin-left: 10%; margin-top: 20%; font-family:calibri">CONTAXTS</h1>
		<p style="color: aliceblue;font-family: Calibri; margin-top:23%">TM</p> 
	</div>
		<img on:click={displayInputFormPage} on:keydown style="margin:40px;cursor: pointer" src="/plusicon.png" alt="add" > 
	</div>
{#each contacts as contact,index}
<div on:click={()=>displayContactInfo(contact)} on:keydown key={index} style="Cursor:pointer; color: aliceblue; margin-left:5%; font-size: 22px; font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif">{contact.fullName}</div>
{/each}
</div>
<div style= "margin-top:5%; margin-left:22%;{activeComponent === 'writeUp'? 'display:block':'display:none'}">
	<div class = "contaxtsTitle" >
		<h1 style="color: rgb(48, 113, 116); margin-left: 7%; margin-top: 20%; font-family:calibri; font-size:45px">CONTAXTS</h1>
		<p style="color: rgb(48, 113, 116);font-family: arial; margin-top:26%">TM</p> 
	</div>
	<p style="color: grey; font-family: Calibri;font-size:larger; margin-left: 32%"> Version 0.5</p>
	<h3 style="color: rgb(48, 113, 116); font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;font-size:large;margin-top:30%; margin-left: 10%">EHIMIGBAI MCRICH</h3>
	<h1 style="color: grey; font-family:sans-serif;font-size:large; margin-left: 32%">@McRich1</h1>
</div>
<div class="inputFormPage" style={activeComponent === 'inputFormPage'? 'display:block' : 'display:none'}>
	<div style ="margin-top: 1%">
	<input class = "inputBox" placeholder="Fullname" bind:value={fullName}>
	<p style ="{duplicateError? 'display: flex':'display:none'}; margin-left:30%"> <img src="/error.png" alt="stop">This contact already exists</p> 
	<input class = "inputBox" placeholder="Phonenumber" bind:value={phoneNumber}>
	<input class = "inputBox"placeholder="Email" bind:value={email}>
	<input class = "inputBox"placeholder="Date" type="date" bind:value={date}>
	<input class = "inputBox"placeholder= "Address" bind:value={address}>
	<div><button on:click={clearInputFormPage} on:keydown style="margin-left:30%; cursor:pointer; margin-top:10%">Cancel</button> 
		<button on:click={createContact} on:keydown style="margin-left:20%; cursor:pointer;background-color: rgb(48, 113, 116); color:white">Save</button>
	</div>
</div>
</div>	
<div class= "contactInfoSection" style={activeComponent==='contactInfoSection'?'display:block':'display:none'}>
	<div><img on:click={editContactInfo} on:keydown style= "margin-left:10%; cursor: pointer" src ="/edit2.png" alt="edit"> <img on:click={deleteContact} on:keydown style= "margin-left:30%; cursor: pointer" src ="/trash2.png" alt="trash"></div>
<div class="contactInfo">
	<h1> Name</h1>
	<p>{selectedContact?.fullName}</p>
	<h1> Phonenumber</h1>
	<p>{selectedContact?.phoneNumber}</p>
	<h1> Email</h1>
	<p>{selectedContact?.email}</p>
	<h1>Date</h1>
	<p>{selectedContact?.date}</p>
	<h1>Address</h1>
	<p>{selectedContact?.address}</p>
</div>
</div>
</main>

<style>
	.main{
		display: flex;
		flex-direction: row;
	}
	.contactInfoSection{
		margin-top: 1%;
		width: 65%;
		height: 80vh;
	}
	.contactInfo{
		margin-left: 10%;
		margin-top: 5%;
	}
	.inputBox{
		margin-top:4%; margin-left:20%; width:60% 
	}
	.inputFormPage{
		width:65%;
		height: 100vh;
	}
	.leftSection{
		width: 30%;
		height: 100vh;
		background-color: rgb(48, 113, 116);
	}
	.contaxtsTitle{
		display:flex;
		flex-direction: row;
		justify-content: space-between;
	}
</style>