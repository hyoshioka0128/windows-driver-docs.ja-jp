---
title: Microsoft Bluetooth テストプラットフォーム
description: Bluetooth テストプラットフォーム (BTP) の概要。
ms.assetid: de5723f8-cc32-4660-9694-63f6603e6983
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 71d5f5a327019bc2130f1e8b374bafdb5e2d1897
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528923"
---
# <a name="bluetooth-test-platform-btp-overview"></a>Bluetooth テストプラットフォーム (BTP) の概要

Bluetooth テストプラットフォーム (BTP) は、Bluetooth ハードウェア、ドライバー、およびソフトウェアのテストを自動化するように設計されています。 BTP を使用すると、ホスト (PC) と周辺機器の両方で Bluetooth ラジオを試すことができ、拡張可能なフレームワークを想定しています。

- BTP のハードウェアについては、[サポートされている Btp ハードウェア](testing-BTP-hw.md)で詳しく説明されています。
- サポートされているテストおよびテストプロセスは、 [BTP テスト](testing-BTP-Tests.md)で詳しく説明されています。

![テストの概要-ハードウェアビュー](images/btp-hwOverview.png)

 BTP は、Microsoft のサポートソフトウェアと組み合わせた Traduci ハードウェアプラットフォームで構成されています。 Traduci ハードウェアプラットフォームは、接続されている周辺機器の電源管理と sideband 制御をサポートしています。一方、ソフトウェアパッケージは、テスト、ファームウェアパッケージ、プロビジョニングツールで構成されています。

![テストの概要-ソフトウェアビュー](images/btp-swOverview.png)
