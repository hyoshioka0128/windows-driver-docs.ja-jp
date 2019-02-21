---
title: /一覧表示の切り替え
description: 記憶域証明書の管理の強化されたツールの/List スイッチではすべて、IEEE 1667 準拠の USB ストレージ デバイス、コンピューターに接続されているが一覧表示します。
ms.assetid: ae0e2991-32db-42b3-839d-83b7e2b8b35f
keywords:
- /ドライバー開発ツールのスイッチを一覧表示します。
topic_type:
- apiref
api_name:
- /List
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da7b84a0cf06767ae209e6822168982ad87c8f45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529746"
---
# <a name="list-switch"></a>/一覧表示の切り替え


**/List**拡張記憶域証明書管理ツールのスイッチにはすべて、IEEE 1667 準拠の USB ストレージ デバイス、コンピューターに接続されているが一覧表示されます。 このスイッチは指定された USB ストレージ デバイスに認証サイロ (ASC) の証明書ストア内で (プロパティ) と証明書を一覧表示を使用することもできます。

```
    EhStorCertMgrCmd /List [-Volume:
    VolumeName
    ]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>サブパラ メーター


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-ボリューム:**   
IEEE 1667 準拠の USB ストレージのボリュームの名前。 このパラメーターの書式設定に関する詳細については、次を参照してください。[拡張記憶域証明書の管理ツールの概要](overview-of-the-enhanced-storage-certificate-management-tool.md)します。

**注**IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンド プロンプトで Enter キーを押します。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

使用する場合、 **/list**切り替え、パラメーターを指定せず、ツールはすべての IEEE 1667 準拠 USB ストレージ デバイス、コンピューターに接続されているレポートします。 この場合は、USB ストレージ デバイスのボリューム名のみが報告されます。

特定の USB ストレージ デバイスの詳細については、使用、 **-ボリューム**デバイスを指定するパラメーター。 ここで、ツールは、デバイスに ASC ストア内に存在する証明書を報告します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

この例では、IEEE 1667 準拠 USB ストレージ デバイス、コンピューターに接続されているを一覧表示する方法を示します。

```
EhStorCertMgrCmd /List
```

```
Executing list switch...
Volume Name : \\?\usbstor#ieee1667control&ven_msft&prod_disk_sim_v0.01&rev_0.01#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}
```

この例では、IEEE 1667 準拠 USB 記憶装置の ASC ストア内の証明書の詳細を一覧表示する方法を示します。

```
EhStorCertMgrCmd.exe /List -Volume:"\\?\usbstor#ieee1667control&ven_msft&prod_disk_sim_v0.01&rev_0.01#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```

```
Executing List operation for specified volume name...
## Certificate Subject             : Microsoft Cert Simulator RSA 1024 SHA-1
---------------------------------
Certificate Index               : 0
Issued To                       : Microsoft Cert Simulator RSA 1024 SHA-1
Issued By                       : Microsoft 1667 Simulator Root
Certificate Expiration Date     : 12/30/9999
Certificate Status              : A certificate chain could not be built to a trusted root authority.

## Certificate Subject             : PCp PKCS SHA-1 1024 no ext
---------------------------------
Certificate Index               : 1
Issued To                       : PCp PKCS SHA-1 1024 no ext
Issued By                       : PCp PKCS SHA-1 1024 no ext
Certificate Expiration Date     : 5/31/2010
Certificate Status              : Certificate is Valid

## Certificate Subject             : HCh PKCS SHA-1 1024 no ext
---------------------------------
Certificate Index               : 2
Issued To                       : HCh PKCS SHA-1 1024 no ext
Issued By                       : HCh PKCS SHA-1 1024 no ext
Certificate Expiration Date     : 5/31/2010
Certificate Status              : Certificate is Valid
```









