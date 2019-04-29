---
title: .enumtag (セカンダリ コールバック データの列挙)
description: .Enumtag コマンドでは、セカンダリのバグ チェック コールバックのデータとデータのすべてのタグが表示されます。
ms.assetid: 2146ebb9-96ce-4eb0-8c23-c9aaa5ed7f73
keywords:
- .enumtag (セカンダリ コールバック データを列挙する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enumtag (Enumerate Secondary Callback Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9987446b2e863e298d6a223b1533185ade168aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336778"
---
# <a name="enumtag-enumerate-secondary-callback-data"></a>.enumtag (セカンダリ コールバック データの列挙)


**.Enumtag**コマンドは、セカンダリのバグ チェック コールバックのデータとデータのすべてのタグが表示されます。

```dbgcmd
.enumtag 
```

## <span id="ddk_meta_enumerate_secondary_callback_data_dbg"></span><span id="DDK_META_ENUMERATE_SECONDARY_CALLBACK_DATA_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
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

詳細については、およびこのデータを表示するには、他の方法については、「[バグ チェック コールバック データの読み取り](reading-bug-check-callback-data.md)します。

<a name="remarks"></a>注釈
-------

使用することができます、 **.enumtag**バグ チェックが行われた後にのみ、またはカーネル モードのクラッシュ ダンプ ファイルをデバッグするときにコマンド。

セカンダリのバグの各ブロックのコールバックのデータを確認、 **.enumtag**コマンド (ASCII 文字の前のバイトとして) (GUID 形式) でタグと、データを表示します。

次の例を検討してください。

```dbgcmd
kd> .enumtag
{87654321-0000-0000-0000000000000000} - 0xf9c bytes
  4D 5A 90 00 03 00 00 00 04 00 00 00 FF FF 00 00  MZ..............
  B8 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00  ........@.......
  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
  ....
  00 00 00 00 00 00 00 00 00 00 00 00              ............

{12345678-0000-0000-0000000000000000} - 0x298 bytes
  F4 BF 7B 80 F4 BF 7B 80 00 00 00 00 00 00 00 00  ..{...{.........
 4B 44 42 47 98 02 00 00 00 20 4D 80 00 00 00 00  KDBG..... M.....
  54 A5 57 80 00 00 00 00 A0 50 5A 80 00 00 00 00  T.W......PZ.....
 40 01 08 00 18 00 00 00 BC 7D 50 80 00 00 00 00  @........}P.....
  ....
  00 00 00 00 00 00 00 00                          ........
```

この例では、セカンダリ データの最初のバッチは、GUID を持つ){87654321-0000-0000-0000000000000000}) データのバッチが GUID をそのタグと、2 つ目 ({12345678-0000-0000-0000000000000000}) タグとして。 ただし、データには有用な形式でないです。

 

 





