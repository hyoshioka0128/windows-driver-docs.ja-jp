---
title: KsInvalidStreamPointer rule (ks)
description: このルールは、KS ミニポートドライバーが関数の引数として有効な KS ストリームポインターを提供するかどうかを確認します。
ms.assetid: C9BBF9A6-3F0A-4494-BA13-A9CD55969979
ms.date: 04/01/2020
keywords:
- KsInvalidStreamPointer rule (ks)
topic_type:
- apiref
api_name:
- KsInvalidStreamPointer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cb906f388d290f5fe58542b132026f89a03573d9
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968173"
---
# <a name="ksinvalidstreampointer-rule-ks"></a>KsInvalidStreamPointer rule (ks)

**Ksinvalidstreampointer** rule は、ks ミニポートドライバーが有効な Ks ストリームポインターを関数の引数として提供するかどうかを確認します。 一般的な違反は、不適切なポインター処理、またはメモリの不適切な使用によって発生するポインターの破損によって発生します。

有効なストリームポインターは、先頭または末尾のエッジストリームポインター、または[Ksk Streampointer clone](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)を介して複製されたストリームポインターです。 詳細については[、「先頭および末尾のエッジストリームポインター](
https://docs.microsoft.com/windows-hardware/drivers/stream/leading-and-trailing-edge-stream-pointers)」を参照してください。

また、このルールは、コピーされていないストリームポインターを削除しようとしたときに、 [Ksstreampointer delete](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)が使用されていないことを確認します。

**ドライバーモデル: KS**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0008100c)


<a name="example"></a>例
-------

次のコードは、このルールに違反しています。

```cpp
PKKSSTREAM_POINTER StreamPointer = KsPinGetLeadingEdgeStreamPointer (Pin, KSSTREAM_POINTER_STATE_UNLOCKED);

//
// ERROR: KsStreamPointerDelete can only be called on clone stream pointers.
//

KsStreamPointerDelete (StreamPointer);
```

このコードも規則に違反します。 

```cpp
KsStreamPointerDelete (NULL);
```

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 ドライバー検証ツールコマンドを入力し、「 <strong>/domain ks</strong>」と指定します。</p>
<p>次に例を示します。</p>
<p></p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

**検証ツール (/domain** \[ )*オプション* \]**/driver** * &lt; ドライバー &gt; *の/driver

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

Ksstreamポインターの削除

Ksstreamポインターの詳細

KsStreamPointerAdvanceOffsetsAndUnlock

Ksstreamポインター Canceltimeout

Ksstreamポインター Getirp

Ksstreamポインター Getmdl

KsStreamPointerGetNextClone

KsStreamPointerLock

Ksstreamポインタ Scheduletimeout

Ksstreamポインター Setstatuscode

KsStreamPointerUnlock
