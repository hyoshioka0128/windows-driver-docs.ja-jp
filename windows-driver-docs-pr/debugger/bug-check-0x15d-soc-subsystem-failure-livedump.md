---
title: バグ チェック 0x15D SOC_SUBSYSTEM_FAILURE_LIVEDUMP
description: SOC_SUBSYSTEM_FAILURE_LIVEDUMP バグのコードでは、0x0000015D の値を持ちます。
ms.assetid: F7903E88-1706-46E6-A5D0-6972702058A8
keywords:
- バグ チェック 0x15D SOC_SUBSYSTEM_FAILURE_LIVEDUMP
- バグ チェック 0x14B SOC_SUBSYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Bug Check 0x14B SOC_SUBSYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa981557ef1b7328d6a90268bf2a7cb3e8e9c486
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520015"
---
# <a name="bug-check-0x15d-socsubsystemfailurelivedump"></a>バグ チェック 0x15D:SOC\_サブシステム\_エラー\_LIVEDUMP


SOC\_サブシステム\_エラー\_LIVEDUMP バグ コードが 0x0000015D の値を持ちます。 これは、チップ (SoC) サブシステム上のシステムが重大な障害が発生したし、ライブ カーネル ダンプをキャプチャしたことを示します。 SoC のサブシステムでは、このような状況でのバグ チェックは生成されません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


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
<td align="left"><p>アドレス、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_soc_subsystem_failure_details" data-raw-source="[SOC_SUBSYSTEM_FAILURE_DETAILS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_soc_subsystem_failure_details)">SOC_SUBSYSTEM_FAILURE_DETAILS</a></strong>構造体。</p></td>
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

<a name="requirements"></a>必要条件
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

 

 




