---
title: デバイスのプラグイン WDTF 単純な I/O の書き込み
description: デバイスの基本的なテストから最大限の利点を取得するには、デバイスに簡単な I/O プラグインは、デバイスに簡単な I/O を実行できることが必要です。
ms.assetid: FAC4D538-4C2B-46C1-B971-63FF66C2922B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51dc254ab2a6bcfb3deb6fa4f6db1c90ce12ef7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578059"
---
# <a name="writing-a-wdtf-simple-io-plug-in-for-your-device"></a>デバイスのプラグイン WDTF 単純な I/O の書き込み

[デバイスの基本テスト](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-select-and-configure-the-device-fundamental-tests)のメリットを最大限に引き出すには、デバイスへのシンプル I/O を実行できるシンプル I/O プラグインがデバイスに必要です。 これには、WDTF に付属する既定のいずれかのシンプル I/O プラグまたはユーザーが作成した I/O プラグを使用できます。 デバイスの種類がサポートされているかどうかと、テストに固有の要件があるかどうかを確認するには、「[提供されている WDTF シンプル I/O プラグイン](provided-wdtf-simpleio-plug-ins.md)」をご覧ください。

Visual Studio を使用したテストのテスト コンピューターを構成した場合、テスト コンピューター WDTF の単純な I/O をサポートしているデバイスの一覧を返しますのテストを実行できます。 デバイスがサポートされていない場合は、Visual Studio を使用して 1 つを作成、 **WDTF 単純な I/O 操作プラグイン**テンプレート。 詳しくは、次を参照してください。 [WDTF 単純な I/O 操作のプラグインを使用してデバイスの I/O をカスタマイズする方法](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)します。 テスト コンピューターの設定の詳細については、次を参照してください。[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。

## <a name="in-this-section"></a>このセクションの内容

- [カスタム WDTF 単純な I/O 操作のプラグインが、デバイスに必要なかどうかを判断する方法](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)

- [WDTF シンプル I/O アクション プラグインを使ってデバイスの I/O をカスタマイズする方法](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)

- [WDTF SimpleIO プラグインを提供](provided-wdtf-simpleio-plug-ins.md)
