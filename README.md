# sendfriendscircle
wxbot,个人微信PC版hook发朋友圈源码api接口,windows版微信Hook开发SDK之C#版-微信二次开发，PC个人企业微信机器人之实战分析微信发送xml文章消息call，微信机器人开发sdk，个人微信机器人开发API，淘宝客微信发单机器人开发sdk，导购返利机器人研发SDK、微信群管理机器人开发SDK， 微信二次开发SDK，微信个人号开发API接口协议企业微信SDK、企业微信开发API、,企业微信第三方开发接口适用于企业微信营销软件研发、企业微信工作手机研发、企业微信云控系统研发、企业微信客服系统研发、企业微信营销系统研发、 企业微信客微商营销工具研发、企业微信scrm客服系统研发、企业微信聊天机器人、企业微信群管理机器人研发企业微信协议API接口开发
通过hookPC个微内存调用函数，实现各种方便的功能，支持各种开发语言调用，现已实现的功能：
发各种文本，图片，小程序，视频，XML等消息，
接收各种消息，加好友，群管理，收藏信息操作，获取朋友圈列表，点赞，评论，发朋友圈 等等功能接口，无限更新中

部分c++代码示例：


Void SendFriendMsg(std::wstring wxid, std::wstring text)
{
	DWORD call1 = m_WeChatWinHandle + WxSendFriendMsgCallOff;

	stWxMesText asmId(wxid);
	stWxMesText asmText(text);

	char buf1[0x500] = { 0 };
	char buf2[0x900] = { 0 };

	__asm 
	{
		lea eax, buf1;
		push 1;
		push eax;
		lea edi, asmText;
		push edi;
		lea  edx, asmId;
		lea ecx, buf2;
		call call1;
		add esp, 0xC;
	}

}

void  __declspec(naked) ShowImg()
{
	//备份寄存器
	__asm pushmdad;
	__asm pushwdfd;
	//取出ecx的内容
	__asm mov pEcx, ecx;
	SaveImg(pEcx);
	//恢复寄存器
	__asm pushwdfd;
	__asm pushmdad;

	//跳转到返回地址
	__asm jmp dwRetAddr;
}


void SaveImg(DWORD qrcode)
{
	//获取图片长度
	DWORD dwPicLen = qrcode + 0x4;
	size_t cpyLen = (size_t)*((LPVOID*)dwPicLen);
	//拷贝图片的数据
	char PicData[0xFFF] = { 0 };
	memcpy(PicData, *((LPVOID*)qrcode), cpyLen);

	char szTempPath[MAX_PATH] = { 0 };
	char szPicturePath[MAX_PATH] = { 0 };
	GetTempPathA(MAX_PATH, szTempPath);

	sprintf_s(szPicturePath, "%s%s", szTempPath, "qrcode.png");
	//将文件写到Temp目录下
	HANDLE hFile = CreateFileA(szPicturePath, GENERIC_ALL, 0, NULL, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL, NULL);
	if (hFile == NULL)
	{
		MessageBoxA(NULL, "创建图片文件失败", "错误", 0);
		return;
	}

	DWORD dwRead = 0;
	if (WriteFile(hFile, PicData, cpyLen, &dwRead, NULL) == 0)
	{
		MessageBoxA(NULL, "写入图片文件失败", "错误", 0);
		return;
	}
	CloseHandle(hFile);
	
	//完成之后卸载HOOK
	UnHookQrCode(QrCodeOffset);

}


![image](https://user-images.githubusercontent.com/96330669/176147168-09856259-4f54-47b7-b288-5d2c4d56e863.png)



欢迎技术交流：

HWND Qq[]=“2645542961”;
wchar_t tempbuff[0x1024];
个微：
目前已经实现了很多有趣的功能，运行稳定，比如：发各种消息，
接收各种消息，群管，下载文件，加好友，检测僵尸粉，朋友圈等等功能，
可提供接口，方便各种语言二次开发，欢迎技术交流，Q：2645542961
，请勿用于商业用途。


企业微信：
目前已经实现了大部分功能，运行稳定，比如：发各种消息，
接收各种消息，外部群内部群管理，下载文件，加好友等等功能，
可提供接口，方便各种语言二次开发，欢迎技术交流。
请勿用于商业用途。


