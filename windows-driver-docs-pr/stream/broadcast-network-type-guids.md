---
title: ブロードキャスト ネットワーク型の Guid
description: ブロードキャスト ネットワーク型の Guid
ms.assetid: 3501cb1f-10f7-481b-bd2f-1f77156a676a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8954f78d9e0b6fcb82e90f4683dc3fc32c1ed38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557356"
---
# <a name="broadcast-network-type-guids"></a>ブロードキャスト ネットワーク型の Guid


AVStream、ミニドライバーでは、ネットワークの種類の Guid を使用して、スキャン操作をサポートするブロードキャスト ネットワークの種類を指定します。 *Bdamedia.h*ヘッダー ファイルには、これらの Guid が定義されています。 サポートされているネットワークの種類のスキャン機能を取得する方法の詳細については、次を参照してください、 [ **KSPROPERTY\_チューナー\_スキャン\_CAP** ](ksproperty-tuner-scan-caps.md)と。[**KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP** ](ksproperty-tuner-networktype-scan-caps.md)プロパティ。

次のネットワークの種類の Guid は BDA で使用できます。

<span id="ANALOG_AUXIN_NETWORK_TYPE"></span><span id="analog_auxin_network_type"></span>アナログ\_AUXIN\_ネットワーク\_型  
補助的な信号をアナログのブロードキャスト ネットワークの種類。

<span id="ANALOG_FM_NETWORK_TYPE"></span><span id="analog_fm_network_type"></span>ANALOG\_FM\_NETWORK\_TYPE  
ブロードキャスト (FM) ラジオの頻度で変調されたネットワークの種類を通知します。

<span id="ANALOG_TV_NETWORK_TYPE"></span><span id="analog_tv_network_type"></span>アナログ\_テレビ\_ネットワーク\_型  
アナログ テレビ信号をブロードキャストするネットワークの種類。

<span id="DIGITAL_CABLE_NETWORK_TYPE"></span><span id="digital_cable_network_type"></span>デジタル\_ケーブル\_ネットワーク\_型  
デジタル信号をケーブルでブロードキャスト ネットワークの種類。

 

 





