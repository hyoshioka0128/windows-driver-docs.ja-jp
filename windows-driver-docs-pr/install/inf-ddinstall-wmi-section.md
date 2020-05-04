---
title: INF DDInstall.WMI セクション
description: INF DDInstall. WMI セクションには、ドライバーが提供する各 WMI クラスの特性を指定する、1つ以上のインターフェイスディレクティブが含まれています。
ms.assetid: 8c4f6b2b-c2b4-4579-9dce-4436e041ebbc
keywords:
- INF DDInstall. WMI セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.WMI Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea23fc30240c2839742bff609d963556c306dd00
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223220"
---
# <a name="inf-ddinstallwmi-section"></a>INF DDInstall.WMI セクション


INF *Ddinstall*。**Wmi**セクションには、ドライバーが提供する各 WMI クラスの特性を指定する、1つ以上の**インターフェイス**ディレクティブが含まれています。

```inf
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

<a href="" id="flags"></a>*示す*  
次のビットマスクフラグのいずれかを指定します。

<a href="" id="0x00000001--scwmi-clobber-security-"></a>0x00000001 (SCWMI_CLOBBER_SECURITY)  
設定されていて、セキュリティ記述子が既にレジストリに存在する場合、既存のセキュリティ記述子は INF ファイルで指定されているものに置き換えられます。 設定されていない場合、およびセキュリティ記述子が既にレジストリに存在する場合は、INF ファイルで指定されているものではなく、既存のセキュリティ記述子が使用されます。

<a href="" id="wmi-class-section"></a>*WMI クラスセクション*  
WMI クラスの特性を設定するためのディレクティブを含む INF ファイルセクションを指定します。

次のディレクティブは、 *WMI クラスセクション*内で指定できます。

<a href="" id="security--security-descriptor-string-"></a>**Security = "**<em>セキュリティ記述子-文字列</em>**"**  
レジストリに格納され、 *WmiClassGUID*によって指定された GUID に適用されるセキュリティ記述子を指定します。 このセキュリティ記述子は、クラスに関連付けられたデータブロックにアクセスするために必要なアクセス許可を指定します。 *セキュリティ記述子文字列*の値は、DACL (**D:**) セキュリティコンポーネントを示すトークンを含む文字列です。

**セキュリティ**エントリは1つだけ存在できます。 複数の**セキュリティ**エントリが存在する場合は、WMI クラスにセキュリティが設定されていません。

<a name="remarks"></a>解説
-------

INF <em>Ddinstall</em>**。WMI**セクションは、Microsoft Windows Server 2003 以降のバージョンのオペレーティングシステムで使用できます。

セキュリティ記述子は、すべての WMI GUID に関連付けられています。 Windows XP 以前のバージョンのオペレーティングシステムでは、WMI Guid の既定のセキュリティ記述子により、すべてのユーザーにフルアクセスが許可されます。 Windows Server 2003 以降のバージョンでは、既定のセキュリティ記述子により、管理者のみにアクセスが許可されます。

ドライバーが WMI クラスを定義していて、既定の記述子を使用しない場合は、 <em>Ddinstall</em>を含め**ます。WMI**セクションでは、レジストリに格納されているセキュリティ記述子を指定し、システムの既定の記述子を上書きします。

INF ファイルでセキュリティ記述子を指定する方法の詳細については、「[セキュリティで保護されたデバイスのインストールの作成](creating-secure-device-installations.md)」を参照してください。

<a name="examples"></a>例
--------

次の例は、単一の<em>Ddinstall</em>を示して**います。** 2 つの Wmi**インターフェイス**ディレクティブを含む WMI セクション。 各ディレクティブは、WMI クラスを識別し、クラスの*wmi クラスセクション*を指定します。

```inf
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

 

 






