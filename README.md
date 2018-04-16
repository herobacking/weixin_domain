# weixin_domain
微信域名检测接口、微信网址检测是否被封、微信网址安全检测、微信网址防封、微信域名防止拦截
# 加QQ群交流： 537573403


function do_check(){
	$domain =  "www.baidu.com";
	//username = 您的用户名   password = 您的密码
	$api_url = "http://vcweixin.com:1337?username=xxx&password=xxx&url=".json_encode($domain);
	$content = get_msg($api_url);
	$data = json_decode($content,true);


	if($data['status']==2){
	    echo "错误：".$data['errmsg'];
	}else if($data['status']==0){
	    echo "域名正常";
	}else if($data['status']==1){
	    echo "域名被封";
	}

}

function get_msg($url){
		$ch = curl_init();
		curl_setopt($ch,CURLOPT_TIMEOUT,5);
		curl_setopt($ch,CURLOPT_RETURNTRANSFER, 1);
		curl_setopt($ch,CURLOPT_URL,$url);
		curl_setopt($ch,CURLOPT_SSL_VERIFYPEER,false);
		curl_setopt($ch,CURLOPT_SSL_VERIFYHOST,false);
		$data = curl_exec($ch);
		if($data){
			curl_close($ch);
			return $data;
		}else {
			$error = curl_errno($ch);
			curl_close($ch);
			return false;
	}
}

do_check();


