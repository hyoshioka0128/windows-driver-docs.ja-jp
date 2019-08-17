---
title: MB id のモーフィングの概要
description: MB デバイスドライバーの id のモーフィングについて説明します。
ms.assetid: 7AA14A5E-47AA-4A9A-94A4-769F374EA465
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6116a3a11b7794bb53cf67ff9eafb7f995a29e4f
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565660"
---
# <a name="introduction-to-mb-identity-morphing"></a>MB Id のモーフィングの概要


## <a name="identity-morphing"></a>Id のモーフィング


モバイルブロードバンド USB ドングルソリューションを使用すると、ドライバーパッケージを含む USB デバイス自体に記憶域機能を持たせることで、モバイルブロードバンドおよびその他の IHV 機能用のドライバーパッケージを別のメディア (CD-ROM など) を介して配布する必要がなくなります。

Windows でこのようなデバイスを初めて挿入すると、デバイスは大容量記憶装置として表示され、ユーザーに Windows 自動再生ダイアログが表示されます。 この時点で、デバイスは、ドライバーソフトウェアが不足しているため、他の機能がユーザーに非機能として表示されないようにするために、大容量記憶装置機能を除く他の機能をホストに公開しません。 ユーザーは、ドライバーパッケージをインストールする IHV 提供のソフトウェアを実行できます。 また、ドライバーパッケージをインストールするだけでなく、IHV が提供するソフトウェアもデバイスを morphs して、他の機能をユーザーに公開します。

Windows 8 に挿入されたときに前述のメカニズムを使用するモバイルブロードバンドデバイスは、大容量記憶装置として機能します。 Windows 8 では、MBIM 仕様に準拠したモバイルブロードバンド機能がネイティブでサポートされているため、ユーザーがモバイルブロードバンド機能を使用するためにドライバーパッケージをインストールする必要はありません。 このセクションのサブトピックでは、Windows 8 向けにこのソリューションを実装する方法について説明します。これにより、ユーザーは、ドライバーパッケージをインストールしなくても、モバイルブロードバンドデバイスを使用できるようになります。

モーフィング動作を示すモバイルブロードバンドデバイスは、このセクションのサブトピック全体で "モーフィングデバイス" と呼ばれます。

[Mb id のモーフィングソリューションの概要](mb-identity-morphing-solution-overview.md)
[mb id のモーフィングソリューションの詳細](mb-identity-morphing-solution-details.md)
 

 





