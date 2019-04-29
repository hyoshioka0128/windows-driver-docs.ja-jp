---
title: バグ チェック 0x14B SOC_SUBSYSTEM_FAILURE
description: SOC_SUBSYSTEM_FAILURE のバグ チェックでは、0x0000014B の値を持ちます。 これは、チップ (SoC) サブシステム上のシステムに回復不能なエラーが発生したことを示します。
ms.assetid: CC42D634-90CE-43F1-8552-E5DE711D2117
keywords:
- バグ チェック 0x14B SOC_SUBSYSTEM_FAILURE
- バグ チェック 0x14B SOC_SUBSYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Bug Check 0x14B SOC_SUBSYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64388ae3a95bb6aa67b225545637290bbf023457
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335581"
---
# <a name="bug-check-0x14b-socsubsystemfailure"></a>バグ チェック 0x14B:SOC\_サブシステム\_エラー


SOC\_サブシステム\_エラーのバグ チェックが 0x0000014B の値を持ちます。 これは、チップ (SoC) サブシステム上のシステムに回復不能なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="bug-check-0x14b-socsubsystemfailure-parameters"></a>バグ チェック 0x14B SOC\_サブシステム\_エラー パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>アドレス、 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/dn376404" data-raw-source="[SOC_SUBSYSTEM_FAILURE_DETAILS](https://msdn.microsoft.com/library/windows/hardware/dn376404)">SOC_SUBSYSTEM_FAILURE_DETAILS</a></strong>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>(省略可能)。 ベンダーから提供されたデータ ブロックのアドレス。</p></td>
</tr>
</tbody>
</table>

 

<a name="resolution"></a>解決方法
----------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

```dbgcmd
2: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

SOC_SUBSYSTEM_FAILURE (14b)
A SOC subsystem has experienced an unrecoverable critical fault.
Arguments:
Arg1: 9aa8d630, nt!SOC_SUBSYSTEM_FAILURE_DETAILS
Arg2: 00000000, Reserved
Arg3: 00000000, Reserved
Arg4: a126c000, (Optional) address to vendor supplied general purpose data block.
```

指定された nt を使用します。SOC\_サブシステム\_エラー\_dt コマンドと Arg1 によって提供されるアドレスを使用して、エラー データをダンプする詳細の構造体。

```dbgcmd
2: kd> dt nt!SOC_SUBSYSTEM_FAILURE_DETAILS 9aa8d630
   +0x000 SubsysType       : 1 ( SOC_SUBSYS_AUDIO_DSP )
   +0x008 FirmwareVersion  : 0
   +0x010 HardwareVersion  : 0
   +0x018 UnifiedFailureRegionSize : 0x24
   +0x01c UnifiedFailureRegion : [1]  "F"
```

さらに、省略可能な仕入先など、データを解析する SoC ベンダーとの作業では、汎用データ ブロックを提供します。

使ってスタック トレースを確認することも、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。 すべてのプロセッサでスタックを確認するプロセッサ数を指定できます。

また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   システム製造元から提供されたハードウェア診断を実行して確認することができます。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
</tbody>
</table>

 

 




