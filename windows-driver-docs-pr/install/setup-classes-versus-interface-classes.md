---
title: Windows のクラスとします。インターフェイス クラス
description: Windows のクラスとします。
ms.assetid: 3df99388-6fcf-44bb-a6c9-99281a8879d7
keywords:
- デバイスのインターフェイス クラス WDK デバイスのインストール
- デバイス セットアップ クラス WDK デバイスのインストール
- インターフェイス クラス WDK デバイスのインストール
- セットアップ クラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b198fa199fb150ac663df24da7ab01a074a0e02d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386395"
---
# <a name="windows-classes-vs-interface-classes"></a>Windows のクラスとします。インターフェイス クラス





デバイス クラスの 2 つの種類を区別することが重要: [*デバイス インターフェイス クラス*](device-interface-classes.md)と[*デバイス セットアップ クラス*](device-setup-classes.md)します。 2 つを簡単に混乱することがユーザー モードでコードの同じセット[デバイス インストールの機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))とデータ構造の同じセット ([デバイス情報設定](device-information-sets.md)) 両方のクラスで使用されます。 さらに、デバイスを多くの場合が属しているセットアップ クラスとインターフェイスのいくつかのクラスの両方に同時にします。 それにもかかわらず、クラスの 2 つの種類はさまざまな目的、レジストリでは、さまざまな領域の使用と異なる一連のクラスの Guid を定義するためのヘッダー ファイルに依存します。

[デバイス セットアップ クラス](device-setup-classes.md)がインストールされ、同じ方法で構成されているデバイスをグループ化するためのメカニズムを提供します。 クラスのインストーラーとクラスの co-installer をクラスに属しているデバイスのインストールに関連するセットアップ クラスを識別します。 などすべての CD-ROM ドライブは CDROM セットアップ クラスに属しているし、インストールされている場合は、同一の共同インストーラーを使用します。

[デバイスのインターフェイス クラス](device-interface-classes.md)特性を共有するに従って、デバイスをグループ化するためのメカニズムを提供します。 個々 のデバイスのシステムの存在を追跡するのではなく到着または特定のインターフェイス クラスに属する任意のデバイスの削除の通知を受け取るドライバーとアプリケーションのユーザーを登録できます。

Windows クラスは、システムのファイルで定義されている*Devguid.h*します。 このファイルは、セットアップ クラスの一連の Guid を定義します。 ただし、デバイス セットアップ クラスはで表されます。 *Devguid.h*デバイスと混同しない必要があります*インターフェイス*クラス。 *Devguid.h*ファイルには、セットアップ クラス Guid にはのみが含まれています。

インターフェイス クラスの定義は、1 つのファイルは提供されません。 デバイスのインターフェイス クラスは常に、デバイスの特定のクラスにのみ属しているヘッダー ファイルで定義します。 たとえば、 *Ntddmou.h* GUID_CLASS_MOUSE、マウス インターフェイス クラスを表す GUID の定義が含まれています*Ntddpar.h*並列デバイスのインターフェイス クラス GUID を定義します。*Ntddpcm.h* PCMCIA デバイス; の標準的なインターフェイス クラス GUID を定義します*Ntddstor.h* 、記憶装置のインターフェイス クラス GUID を定義します。

デバイスのインターフェイスのインスタンスの追加の通知に登録するには、デバイスのインターフェイス クラスに固有のヘッダー ファイル内の Guid を使用してください。 ドライバーは、インターフェイス クラス GUID の代わりに、セットアップ クラス GUID を使用して通知の登録場合、しには通知されませんインターフェイスが到着したとき。

新しいセットアップ クラスまたはインターフェイスのクラスを定義するときに*セットアップ クラスとインターフェイス クラスの両方を識別するために単一の GUID を使用しないでください。*

Guid の詳細については、次を参照してください。[ドライバーを使用して Guid](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)します。

 

 





