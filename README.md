(function(){
	var win1 = Titanium.UI.createWindow({
		title:'Select Color',
		backgroundColor:'fff'
	});
	win1.open();
var Teas = ['#F5F5DC', '#FFE4B5', '#FFE4C4', '#D2B48C',
'#C3B091', '#C3B091', '#926F5B', '#804000', '#654321', '#3D2B1F'];
allRows = [];
var theColours = Titanium.UI.createTableView({});
for (var i=0; i<Teas.length; i++){
	theRow = Titanium.UI.createTableViewRow({
		backgroundColor: Teas[i],
		height:50,
		TeaColour:Teas[i]});
		allRows.push(theRow);
	}
theColours.setData(allRows);
win1.add(theColours);

function getVerdict(Colour){
	var indicator = Colour.charAt(1);
	var msg;
	switch(indicator){
		case 'F': msg = 'Milky'; break;
		case 'D': msg = 'Nice'; break;
		case 'C': msg = 'Perfect'; break;
		case '9': msg = 'A bit strong'; break;
		case '8': msg = 'Builders tea'; break;
		case '6': msg = 'Send it back'; break;
		case '3': msg = 'No milk here'; break;
	}
	return msg;
};
function showTeaVerdict(_args){
	var teaVerdict = Titanium.UI.createWindow({
		layout:'vertical'});
		teaVerdict.backgroundColor = _args;
		teaVerdict.msg = getVerdict(_args);
		var  judgement = Titanium.UI.createLabel
		({text:teaVerdict.msg, top:'50%'});
		var close = Titanium.UI.createButton
		({title:'Choose again', top:'25%'});
		close.addEventListener('click', function(e)
		{teaVerdict.close();
			teaVerdict = null;
	});
	teaVerdict.add(judgement);
	teaVerdict.add(close);
	teaVerdict.open();
}
theColours.addEventListener('click', function(e)
{showTeaVerdict(e.source.TeaColor);
	});

var win2 = Titanium.UI.createWindow({
	title: 'Select Color',
	backgroundColor: '#fff'
});

var NavButton1 = Titanium.UI.createButton({
	title: 'Camera',
	color: '#FFFFFF',
	width: '100%',
	top: 500,
	height: 40,
	backgroundColor: '#000000',
	font: {fontSize:'30sp', fontWeight:'bold'},
});
win1.add(NavButton1);
NavButton1.addEventListener('click', function(){
	win2.open();
});

var win2 = Titanium.UI.createWindow({
	backgroundColor:'#FFF'
});

var NavButton2 = Titanium.UI.createButton({
	title:'Tea',
	color: '#FFFFFF',
	top: 500,
	width:'100%',
	height: 40,
	backgroundColor:'#000000',
	font:{fontSize:'30sp', fontWeight:'bold'}
});
win2.add(NavButton2);
NavButton2.addEventListener('click', function(){
	Titanium.API.info('Clicked Home Button');
	win2.close();
});

var options = Titanium.UI.createView({layout: 'vertical'});
var showCamera = Titanium.UI.createButton({ title: 'Show Camera'});
var thePhoto = Titanium.UI.createImageView({height: '30%', width: '30%'});

});

options.add(showCamera);
options.add(thePhoto);
win1.add(options);

function showPhoto(_args){
	thePhoto.setImage(_args.media);
}
showCamera.addEventListener('click', function(e){
	Titanium.Media.showCamera({animated: true,
		autoHide: true,
		saveToPhotoGallery: true,
		showControls: true,
		mediaTypes: [Titanium.Media.MEDIA_TYPE_PHOTO],
		success: function(e) {showPhoto(e);},
		error: function(e) {alert('There was a problem accessing the camera');}
	});
});
