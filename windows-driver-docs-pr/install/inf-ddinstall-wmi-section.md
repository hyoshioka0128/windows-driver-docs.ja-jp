---
title: INF DDInstall.WMI セクション
description: INF DDInstall.WMI セクションには、ドライバーを提供する各 WMI クラスの特性を指定する 1 つまたは複数の WMIInterface ディレクティブが含まれています。
ms.assetid: 8c4f6b2b-c2b4-4579-9dce-4436e041ebbc
keywords:
- INF DDInstall.WMI セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.WMI Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f02b590e141faf4a96dc6aef12d4bafdd19cb15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572500"
---
# <a name="inf-ddinstallwmi-section"></a>INF DDInstall.WMI セクション


INF *DDInstall*.**WMI**セクションは、1 つ以上含まれています。 **WMIInterface**ディレクティブが、ドライバーを提供する各 WMI クラスの特性を指定します。

```ini
[install-section-name.WMI] |
[install-section-name.nt.WMI] | 
[install-section-name.ntx86.WMI] |
[install-section-name.ntarm.WMI] |  (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.WMI]  (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.WMI] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.WMI]  (Windows XP and later versions of Windows)
 
WMIInterface={WmiClassGUID},[flags,]WMI-class-section
```

## <a name="entries"></a>エントリ


<a href="" id="wmiclassguid"></a>*WmiClassGUID*  
WMI クラスを識別する GUID 値を指定します。

<a href="" id="flags"></a>*フラグ*  
次のビット フラグのいずれかを指定します。

<a href="" id="0x00000001--scwmi-clobber-security-"></a>0x00000001 (SCWMI_CLOBBER_SECURITY)  
場合設定すると、既存のセキュリティ記述子は INF ファイルで指定された 1 つに置き換え、レジストリのセキュリティ記述子が既に存在する場合があるとします。 ない場合、レジストリのセキュリティ記述子が既に存在する場合、既存のセキュリティ記述子は INF ファイルで指定された 1 つではなく使用されます。

<a href="" id="wmi-class-section"></a>*WMI-section クラス*  
WMI クラスの特性を設定するためのディレクティブを含む INF ファイルのセクションを指定します。

内で、次のディレクティブを指定することができます、*セクション クラス-WMI-*:

<a href="" id="security--security-descriptor-string-"></a>**Security="**<em>security-descriptor-string</em>**"**  
レジストリに格納されているで指定された GUID に適用するセキュリティ記述子を指定します*WmiClassGUID*します。 このセキュリティ記述子には、クラスに関連付けられたアクセスのデータ ブロックするために必要なアクセス許可を指定します。 *セキュリティ記述子の文字列*値は、トークンの DACL を示す文字列 (**d:**) セキュリティ コンポーネント。

1 つだけ**セキュリティ**エントリが存在することができます。 1 つ以上の場合**セキュリティ**エントリが存在する、WMI クラスのセキュリティが設定されていません。

<a name="remarks"></a>コメント
-------

INF <em>DDInstall</em>**します。WMI**セクションは、Microsoft Windows Server 2003 およびそれ以降のバージョンのオペレーティング システムで使用します。

セキュリティ記述子は、各 WMI GUID に関連付けられます。 Windows XP や以前のオペレーティング システム バージョンは、WMI の Guid の既定のセキュリティ記述子は、すべてのユーザーへのフル アクセスを許可します。 Windows Server 2003 と以降のバージョンでは、既定のセキュリティ記述子は管理者のみにアクセスできます。

既定の記述子を使用して、含めるたくない場合と、ドライバーには、WMI クラスが定義されている場合、 <em>DDInstall</em>**します。WMI**セクションは、レジストリに格納され、システムの既定の記述子をオーバーライドするセキュリティ記述子を指定します。

INF ファイルのセキュリティ記述子を指定する方法の詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](creating-secure-device-installations.md)します。

<a name="examples"></a>使用例
--------

次の例は、1 つ<em>DDInstall</em>**します。WMI**を含む 2 つのセクション**WMIInterface**ディレクティブ。 各ディレクティブを WMI クラスを識別および指定、*セクション クラス-WMI-* クラス。

```ini
[InstallA.NT.WMI]
WMIInterface = {99999999-4cf9-11d2-ba4a-00a0c9062910},,WMISecurity1
WMIInterface = {99999998-4cf9-11d2-ba4a-00a0c9062910},1,WMISecurity2

[WmiSecurity1]
security = "O:BAG:BAD:(A;;0x120fff;;;BA)(A;;CC;;;WD)(A;;0x120fff;;;SY)"

[WmiSecurity2]
security = "O:BAG:BAD:(A;;0x120fff;;;BA)(A;;CC;;;WD)(A;;0x120fff;;;SY)"
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[***モデル***](inf-models-section.md)

 

 






