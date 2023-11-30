```js
//데이터 변환
function convertToChartMultiKey(dataRows, keyInfo){
	// keyInfo = { key1: keyText1, key2:  keyText2, key3:  keyText3, key4:  keyText4};
	if(dataRows.length == 0) return [{"name" : "no data", "data" : []}];
	
	var series = [];
	var useKeys = [];
	Object.entries(keyInfo).map(([colNm, showText])=>{
		var obj = {'data': showText, 'key': colNm, 'data':[]};
		series.push(obj);
		useKeys.push(colNm);
	});

	dataRows.map((row)=>{
		useKeys.map((key)=>{
			var theSeriesIdx = series.findIndex((s)=> s.key == key );
			if(theSeriesIdx == -1 ) return;
			series[theSeriesIdx]['data'].push(row[key]);
		});
		
	});
	return series;
}

```

#convert-data
