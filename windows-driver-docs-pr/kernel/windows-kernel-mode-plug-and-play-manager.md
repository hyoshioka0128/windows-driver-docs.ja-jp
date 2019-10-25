---
title: Windows カーネルモード プラグ アンド プレイ マネージャー
description: Windows カーネルモード プラグ アンド プレイ マネージャー
ms.assetid: 43d06dbe-da66-4103-8be3-f27ff075a1b4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7df652b5ca96be6c5f2739e0f00db6e432a3a51d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835715"
---
# <a name="windows-kernel-mode-plug-and-play-manager"></a>Windows カーネルモード プラグ アンド プレイ マネージャー


プラグアンドプレイ (PnP) は、ハードウェアテクノロジとソフトウェア手法を組み合わせたもので、デバイスがシステムに追加されたときに PC が認識できるようにします。 PnP を使用すると、ユーザーからの入力をほとんどまたはまったく行わずにシステム構成を変更できます。 たとえば、USB ドライブが電源に接続されている場合、Windows はそのドライブを検出し、自動的にファイルシステムに追加できます。 ただし、ハードウェアは特定の要件に従っている必要があるため、ドライバーが必要です。

ドライバーの PnP の詳細については、「[プラグアンドプレイ](implementing-plug-and-play.md)」を参照してください。

PnP マネージャーは、実際には i/o マネージャーのサブシステムです。 I/o マネージャーの詳細については、「 [Windows カーネルモード I/o マネージャー](windows-kernel-mode-i-o-manager.md)」を参照してください。

PnP ルーチンの一覧については、「[プラグアンドプレイルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

PnP マネージャーに直接インターフェイスを提供するルーチンはないことに注意してください。つまり、"**Pp**" ルーチンは存在しません。

Windows ドライバーフレームワーク (WDF) には、PnP 管理をはるかに簡単にするためのライブラリのセットが用意されています。 WDF の詳細については、「[カーネルモードドライバーフレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)」を参照してください。

 

 




