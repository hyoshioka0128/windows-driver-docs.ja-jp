---
title: .open (ソース ファイルを開く)
description: .Open コマンドでは、ソース ファイルのソース パスを検索し、このファイルを開きます。
ms.assetid: 49944fc8-5ecb-47a4-a046-0df18a242e72
keywords:
- .open (オープン ソース ファイル) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .open (Open Source File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef67ba926a5c6612c7dc30f9281a916b91751788
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334420"
---
# <a name="open-open-source-file"></a>.open (ソース ファイルを開く)


**.Open**コマンドは、ソース ファイルのソース パスを検索し、このファイルを開きます。

```dbgcmd
.open [-m Address] FileName 
.open -a Address 
```

## <a name="span-idddkmetaopensourcefiledbgspanspan-idddkmetaopensourcefiledbgspanparameters"></a><span id="ddk_meta_open_source_file_dbg"></span><span id="DDK_META_OPEN_SOURCE_FILE_DBG"></span>パラメーター


<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
ソース ファイル名を指定します。 この名前は、絶対または相対パスを含めることができます。 絶対パスを指定しない限り、パスは、ソース パスのディレクトリに対して相対的に解釈されます。

<span id="_______-m_______Address______"></span><span id="_______-m_______address______"></span><span id="_______-M_______ADDRESS______"></span> **-m** **** *アドレス*   
ソース ファイル内のアドレスを指定します。 このアドレスは、既知のモジュールに含まれる必要があります。 使用する必要があります、 **-m** **** *アドレス*パラメーター場合、ファイルを*FileName*を指定します一意ではありません。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

**-M**を使用する場合は、パラメーターが必要です、[移行元サーバー](using-a-source-server.md)ソース ファイルを取得します。

<span id="_______-a_______Address______"></span><span id="_______-a_______address______"></span><span id="_______-A_______ADDRESS______"></span> **-** *アドレス*   
ソース ファイル内のアドレスを指定します。 このアドレスは、既知のモジュールに含まれる必要があります。 デバッガーを読み込みますファイルを開きをデバッガーには、ソース ファイルを見つけることができますと、指定したアドレスに対応する行が強調表示されます。 アドレスが表示されます、デバッガーがソース ファイルを見つけられない場合、[逆アセンブル ウィンドウ](disassembly-window.md)します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

使用することができます、 **.open** WinDbg でのみコマンドを使用するとスクリプト ファイルで使用できません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソース ファイルとソース パスの詳細については、およびソース ファイルを読み込むには、他の方法については、「[ソース パス](source-path.md)します。

 

 





