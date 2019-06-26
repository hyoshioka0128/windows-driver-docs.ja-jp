---
title: 永続的なメモリ ウィンドウからアクセス メモリ
description: 永続メモリ ウィンドウを使用して PCMCIA 属性メモリにアクセスする
ms.assetid: 866851b9-8e39-4480-9f22-dc2a2eb80ce0
keywords:
- 属性のメモリ バスの WDK PCMCIA、永続的に割り当てられたメモリ ウィンドウ
- 永続的なメモリ ウィンドウ WDK PCMCIA バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c514ae00c3fd309d306fe83970eb4de448bdf91d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380699"
---
# <a name="access-pcmcia-attribute-memory-through-a-permanent-memory-window"></a>永続メモリ ウィンドウを使用して PCMCIA 属性メモリにアクセスする





このセクションでは、PC カードまたは CardBus カードのドライバーがメモリにアクセスする属性の永続的に割り当てられたメモリ ウィンドウを使用する方法について説明します。

ドライバーは、属性のメモリ内のデバイスの登録を実装している PCMCIA デバイスをサポートするために、このメソッドを使用する必要があります。 このような場合、ドライバーの ISR は通常 IRQL DIRQL で実行中にデバイスのレジスタに高速に直接アクセスを必要です。

ドライバーは、IRQL DIRQL で実行中に、このメソッドを使用できます。

セットアップとプラグ アンド プレイのマネージャーのサポート、 [ **INF DDInstall.LogConfigOverride セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)、プラグを強制してで指定されたリソースを使用する再生マネージャー、 **PcCardConfig**エントリ。 **LogConfigOverride**セクションを格納するログ構成セクションを指定します、 **PcCardConfig**エントリ。 フィールド、 **PcCardConfig**エントリは、必要なメモリ リソースを指定し、属性のメモリのメモリ リソースが使用されます。

 

 





