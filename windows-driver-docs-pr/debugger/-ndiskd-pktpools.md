---
title: ndiskd pktpools
description: 警告この拡張機能は、レガシ NDIS 5.x ドライバー用です。Pktpools 拡張機能は、割り当てられているすべてのパケットプールの一覧を表示します。
ms.assetid: 0aceb22c-17ab-4199-a313-ecbc4c8f0b6e
keywords:
- pktpools Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pktpools
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80db3b048e912c1045b90706dfe31fae10deb586
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593896"
---
# <a name="ndiskdpktpools"></a>!ndiskd.pktpools

**警告**   この拡張機能は、従来の NDIS 5.x ドライバー用です。 [NDIS \_ パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造とそれに関連付けられているアーキテクチャは非推奨となりました。

**! Ndiskd**拡張機能は、割り当てられているすべてのパケットプールの一覧を表示します。

```console
!ndiskd.pktpools
```

### <a name="dll"></a>[DLL]

Ndiskd.dll

### <a name="examples"></a>例

**! Ndiskd pktpools**拡張機能を実行して、システム上で割り当てられているすべてのパケットプールの一覧を表示します。 パケットプールのハンドルはクリックできないことに注意してください。つまり、パケットプールに関する詳細情報を調べることはできません。 これは、NDIS では NDIS 6.0 以降のパケットプールを使用しないため、これらのプールは古いシステム上に存在する可能性があるレガシドライバーに対してのみ割り当てられるためです。 この例のデバッグ対象マシンには、パケットプールが使用されないように、レガシ NDIS 5.x ドライバーがインストールされていません。 この例は、説明を目的としたものです。

```console
3: kd> !ndiskd.pktpools
Pool      Allocator  BlocksAllocated  BlockSize  PktsPerBlock  PacketLength
ffffdf80131d58c0  fffff80f1fbe3e8f   0x1          0x1000     0xa           0x190   ndis!DriverEntry+6af
ffffdf80131d5940  fffff80f1fbe3e71   0x1          0x1000     0xa           0x180   ndis!DriverEntry+691
```

## <a name="see-also"></a>関連項目

[Windows 2000 および Windows XP ネットワーク設計ガイド](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565849(v=vs.85))

[Windows 2000 および Windows XP ネットワークリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565850(v=vs.85))

[NDIS \_ パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))
