---
title: 自動構成のインボックス サポート
description: 自動構成のインボックス サポート
ms.assetid: cd2faef4-96ba-4d11-99f6-90e41ae2e283
keywords:
- 自動構成の WDK プリンター、インボックス サポート
- プリンターの自動構成の WDK プリンター、インボックス サポート
- ボックスの自動構成サポートの WDK プリンター
- 組み込みの自動構成のサポートについての組み込みの自動構成サポート WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3731dbb9b5a6ff6505bcaf7b5050ca2f65705cb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390562"
---
# <a name="in-box-support-for-autoconfiguration"></a>自動構成のインボックス サポート


Windows Vista では、標準の TCP/IP ポート モニタまたは、Web Services for Devices (WSD) ポート モニターを使用して Unidrv および Pscript5 ベースのドライバーは、自動構成のサポートを提供します。 両面印刷ユニットまたはフォントのカートリッジで懸念などのインストール可能な機能についてのクエリに対してのみ、Windows Vista での自動構成のサポートが提供されることに注意してください。 特定の機能のクエリへの応答に、機能のオプションを 1 つだけできますに関するものです。 両面印刷ユニットがインストールされているかどうかに関するクエリの 2 つの応答のいずれかが明確化: 両面印刷ユニットがインストールされているまたはされなかったことです。 そのフォント カートリッジのいずれかを示す応答を生成するフォントについてカートリッジがインストールされているクエリ*A*がインストールされているか、そのフォント カートリッジ*B*がインストールされています。

複数の応答には、自動構成の現在の (バージョン 1) 実装することはできません。 クエリは、機能の 1 つのオプションに制限されています。 つまり、たとえば、クエリに対する応答ことはできませんを提供メディアの両方については、入力トレイのサイズおよびメディアの色。

次のトピックでは、Windows Vista での自動構成のインボックス サポートの活用方法について説明します。

[プリンターのミニドライバーの変更](printer-minidriver-changes.md)

[プリンタ ポート モニターをカスタマイズします。](customizing-the-printer-port-monitors.md)

 

 




