---
title: 永続的なメモリ ウィンドウからアクセス メモリ
description: 永続的なメモリ ウィンドウからアクセス PCMCIA 属性メモリ
ms.assetid: 866851b9-8e39-4480-9f22-dc2a2eb80ce0
keywords:
- 属性のメモリ バスの WDK PCMCIA、永続的に割り当てられたメモリ ウィンドウ
- 永続的なメモリ ウィンドウ WDK PCMCIA バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49e8abfe5a1cffe684580cc30607f967abf28ebd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557244"
---
# <a name="access-pcmcia-attribute-memory-through-a-permanent-memory-window"></a>永続的なメモリ ウィンドウからアクセス PCMCIA 属性メモリ





このセクションでは、PC カードまたは CardBus カードのドライバーがメモリにアクセスする属性の永続的に割り当てられたメモリ ウィンドウを使用する方法について説明します。

ドライバーは、属性のメモリ内のデバイスの登録を実装している PCMCIA デバイスをサポートするために、このメソッドを使用する必要があります。 このような場合、ドライバーの ISR は通常 IRQL DIRQL で実行中にデバイスのレジスタに高速に直接アクセスを必要です。

ドライバーは、IRQL DIRQL で実行中に、このメソッドを使用できます。

セットアップとプラグ アンド プレイのマネージャーのサポート、 [ **INF DDInstall.LogConfigOverride セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547339)、プラグを強制してで指定されたリソースを使用する再生マネージャー、 **PcCardConfig**エントリ。 **LogConfigOverride**セクションを格納するログ構成セクションを指定します、 **PcCardConfig**エントリ。 フィールド、 **PcCardConfig**エントリは、必要なメモリ リソースを指定し、属性のメモリのメモリ リソースが使用されます。

 

 





