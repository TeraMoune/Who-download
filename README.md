# Who-download
Ведёт учёт скачиваний файлов и даёт возможность показать список пользователей скачавших тот или иной файл.

<details>
	<summary>CSS code</summary>
  
```css
/** Who download module **/
.who-download {
	width: 500px;
    margin: 0 auto;
    position: relative;
	background: #FFF;
    padding: 25px 10px 10px;
    border-radius: 3px;
	border: 1px solid #ccc;
}

#who-download ul {
	list-style-type: none;
    margin: 0;
    padding: 0;	
}

#who-download li {
	font: normal 11px/22px Verdana;
	cursor: pointer;
	border-radius: 2px;
	position: relative;
}

#download-list li { padding: 4px; }

#who-download ul li:hover {
	color: #000;
	background-color: #f5f5f8;
}

#who-download li a {
	display: inline-block;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	vertical-align: middle;
	width: 75%;	
}

#who-download li .download-date {
	position: absolute;
	right: 6px;
	top: 4px;
	font: normal 10px/22px Tahoma;
	color: #999;
}

#who-download li img {
	display: inline-block;
	vertical-align: middle;
	height: 22px;
	width: 22px;
	border-radius: 1px;
	margin-right: 5px;
}

#download-list-nav {width: 100px;margin: 0 auto;}
#download-list-nav li {font-size: 20px;font-weight: 700;cursor: pointer;}
#download-list-nav li.disabled {color:#AAA;}
#download-list-nav li:nth-child(1) {float:left}
#download-list-nav li:nth-child(2) {float:right;}
/** Who download END **/
```
</details>

<details>
  <summary>JavaScript code</summary>
 
```javascript
function who_download_list(id, area) {
	
	//ShowLoading();
	$.post( dle_root + 'engine/ajax/controller.php?mod=who_download', {id: id, static_area: area, user_hash: dle_login_hash}, function(data){
		//HideLoading();			
		if( data == 'null' ) {
			
			//Box.InfoNormal('who-download', 'Информация', 'Файл не скачивали', 400, 2000);
			DLEalert('Файл не скачивали', 'Информация');
			
		} else {
			
			$.magnificPopup.open({
				items: {
					src: '<div class="who-download clrfix">'+data+'</div>'
				},
				type: 'inline',
				mainClass: 'mfp-fade',
				removalDelay: 0,
				overflowY: 'hide',
				closeOnBgClick: true,
				callbacks: {
					open: function() { 
						/*new LazyLoad({
							elements_selector: "#download-list img[data-src]",
							threshold: 0,
							load_delay: 250
						});*/
					},
					afterClose: function() {},		 
					beforeClose: function() {}
				}		
				});
		}
		
		});
		return false;	
	
}
```
  
</details>
