---
title: INF ファイル エントリ
description: INF ファイル エントリ
ms.assetid: 8af2cbe7-f249-4e2f-940f-b50bc451cabe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514bdab3fbd599e7c57246a27dc1ecdf7667ecf2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378966"
---
# <a name="inf-file-entries"></a>INF ファイル エントリ





デバイスの microdriver を使用するには、セットアップ情報 (INF) ファイルに追加のエントリが必要です。 最初に、必要があります"MicroDriver"という名前のエントリで、 **DeviceData** INF ファイルのセクション。 (を参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細についてはします)。このエントリは、microdriver を実装する DLL の名前に設定する必要があります。

### <a name="windows-me-inf-file-entries"></a>Windows Me INF ファイルのエントリ

次は Microsoft Windows Millennium Edition (me)、Windows XP、および以降のオペレーティング システムに適用されます。

内の領域で、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) WIA ミニドライバーは、通常は、参照される場合、INF を一覧表示する必要があります*wiafbdrv.dll*ドライバーとして。 これは、WIA ベッドのドライバーを実装するコンポーネントです。

確認します、 [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)両方、microdriver が含まれていますと*wiafbdrv.dll*、Windows CAB ファイルからコピー先です。 INF ファイルの残りの部分では、WIA の他のデバイスの場合と同じです。

### <a name="windows-xp-inf-file-entries"></a>Windows XP の INF ファイルのエントリ

次の情報には、Windows XP 以降が適用されます。 Windows Me INF ファイルでは使用しないでください**Include**と**必要がある**ディレクティブ、ため、このスタイルの INF を使用することはできません。

[ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)ディレクティブを含める必要があります**Include**sti.inf を = です。 さらに、**必要がある**ディレクティブが参照する必要があります**STI します。MICRODRIVERSection**、適切なデバイスの種類のセクションとします。 これは、ために必要な USDClass と CLSID を指定は**AddReg**ので、INF で明示的に含める必要はありませんこれらのディレクティブ。

**注**  を含める必要はありません*wiafbdrv.dll*で、 **CopyFiles**ディレクティブ。

 

Windows Driver Kit (WDK) CD に収録 WIA microdriver に含まれている INF では、この新しいメソッドを使用して、microdriver を参照します。

 

 




