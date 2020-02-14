
function loadSrtFromUrl(data)
	{
	var url;
	url=prompt("Please enter the URL of the SRT or VTT file you want to use");
	if(url!=null&&url!=""&&url!="?srt=null"&&url!="?srt=")
		{
		$.get(suburl+encodeURIComponent(url),
			{
		}
		,function(data)
			{
			var name=url.split('/');
			name=name[(name.length-1)];
			var track=olplayer.addTextTrack("captions",name,name);
			track.mode="showing";
			var parser=new window['WebVTT']['Parser'](window,window['vttjs'],window['WebVTT']['StringDecoder']());
			parser['oncue']=function(cue)
				{
				track.addCue(cue)
			};
			parser['onparsingerror']=function(error)
				{
			};
			parser['parse'](data);
			parser['flush']();
			window.setTimeout(function()
				{
				$('.vjs-menu-item-text > .vjs-icon-placeholder').remove();
				$('.vjs-menu-content').css('max-height','180px');
				$('.vjs-captions-menu-item').css('height','22px');
				$('.vjs-menu-item-text').css('height','22px');
$('.vjs-menu-item:last').after('<li class="vjs-menu-item vjs-captions-menu-item" tabindex="-1" role="menuitemcheckbox" aria-disabled="false" aria-checked="false" style="height: 22px;" onclick="Load()" id="loadSrtFromPc()" style="background-color: black;" class="vjs-subtitles-menu-item"><span class="vjs-menu-item-text">▤ SRT/VTT from PC</span><span class="vjs-control-text"></span></li><li class="vjs-menu-item vjs-captions-menu-item" tabindex="-1" role="menuitemcheckbox" aria-disabled="false" aria-checked="false" style="height: 22px;" onclick="loadSrtFromUrl()" style="background-color: black;" id="url" class="vjs-subtitles-menu-item"><span class="vjs-menu-item-text">▤ SRT/VTT from URL</span><span class="vjs-control-text"></span></li>');
//$('.vjs-menu-item:last').hide();
}
			,500)
		}
		)
	}
}
function loadSrtFromPc()
	{
	var collection=new FileReader;
	collection.onload=function(dataAndEvents)
		{
		if(collection.result.indexOf("-->")!==-1)
			{
			var track=olplayer.addTextTrack("captions",$("#file").prop("files")[0].name,$("#file").prop("files")[0].name);
			track.mode="showing";
			parseSrt(collection.result,function(cue)
				{
				track.addCue(cue)
			}
			);
			$('.vjs-menu-item-text > .vjs-icon-placeholder').remove();
			$('.vjs-menu-content').css('max-height','180px');
			$('.vjs-captions-menu-item').css('height','22px');
			$('.vjs-menu-item-text').css('height','22px')
$('.vjs-menu-item:last').after('<li class="vjs-menu-item vjs-captions-menu-item" tabindex="-1" role="menuitemcheckbox" aria-disabled="false" aria-checked="false" style="height: 22px;" onclick="Load()" id="loadSrtFromPc()" style="background-color: black;" class="vjs-subtitles-menu-item"><span class="vjs-menu-item-text">▤ SRT/VTT from PC</span><span class="vjs-control-text"></span></li><li class="vjs-menu-item vjs-captions-menu-item" tabindex="-1" role="menuitemcheckbox" aria-disabled="false" aria-checked="false" style="height: 22px;" onclick="loadSrtFromUrl()" style="background-color: black;" id="url" class="vjs-subtitles-menu-item"><span class="vjs-menu-item-text">▤ SRT/VTT from URL</span><span class="vjs-control-text"></span></li>');
//$('.vjs-menu-item:last').hide();
}
		else
			{
			alert("Invaid subtitle file")
		}
	};
	collection.readAsText($("#file").prop("files")[0],"ISO-8859-1")
}
function Load()
	{
	$('#file').click()
}
var isNotScrolled = true;
olplayer.on('play', function() {
if(isNotScrolled)
{
$('.vjs-menu-item:last').before('<li class="vjs-menu-item vjs-captions-menu-item" tabindex="-1" role="menuitemcheckbox" aria-disabled="false" aria-checked="false" style="height: 22px;" onclick="Load()" id="loadSrtFromPc()" style="background-color: black;" class="vjs-subtitles-menu-item"><span class="vjs-menu-item-text">▤ SRT/VTT from PC</span><span class="vjs-control-text"></span></li><li class="vjs-menu-item vjs-captions-menu-item" tabindex="-1" role="menuitemcheckbox" aria-disabled="false" aria-checked="false" style="height: 22px;" onclick="loadSrtFromUrl()" style="background-color: black;" id="url" class="vjs-subtitles-menu-item"><span class="vjs-menu-item-text">▤ SRT/VTT from URL</span><span class="vjs-control-text"></span></li>');
//$('.vjs-menu-item:last').hide();
isNotScrolled = false;
}
});
