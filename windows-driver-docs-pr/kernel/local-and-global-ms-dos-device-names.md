---
title: ローカルおよびグローバル MS-DOS デバイス名
description: ローカルおよびグローバル MS-DOS デバイス名
ms.assetid: bfb7e41c-0f80-4cb9-b036-d1b44473f9fb
keywords:
- MS-DOS デバイス名の WDK カーネル
- MS-DOS デバイス名のローカルの WDK カーネル
- グローバル MS-DOS デバイス名の WDK のカーネル
- '\Dosdevices\z コンテキスト WDK カーネル'
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2014768008e5ff4bf42f4ba3544e0a9af4781068
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381368"
---
# <a name="local-and-global-ms-dos-device-names"></a>ローカルおよびグローバル MS-DOS デバイス名

Microsoft Windows 2000 と Windows NT ベースのオペレーティング システムの以降のバージョンの複数のバージョンの管理、 **\dosdevices\z**ディレクトリ。

これらのオペレーティング システムで 1 つである*グローバル*  **\\\dosdevices\z**ディレクトリと複数*ローカル*  **\\\dosdevices\z**ディレクトリ。 グローバル **\\\dosdevices\z**ディレクトリが表示されるシステム全体である MS-DOS デバイス名を保持します。 ローカル **\\\dosdevices\z**ディレクトリには、特定でのみ表示される、MS-DOS デバイス名*ローカル* **\dosdevices\z** *コンテキスト*.

ローカル**\dosdevices\z**コンテキストは、次のとおりです。

-   ログオン セッションごとに独自のローカルで Windows xp 以降、 **\dosdevices\z**コンテキスト。 システム スレッド、および、LocalSystem ユーザーとして実行されている任意のスレッドがローカルで実行されない**\dosdevices\z**コンテキスト。

-   Windows 2000 では、各ターミナル サーバー セッションが、独自のローカル**\dosdevices\z**コンテキスト。 ローカルのコンソール セッションの一部が実行されないように実行している任意のスレッド**\dosdevices\z**コンテキスト。

各スレッドが現在**\dosdevices\z**コンテキストで、スレッドの有効期間を変更することができます。 ローカルで実行していないスレッド**\dosdevices\z**コンテキストがで実行すると、*グローバル* **\dosdevices\z** *コンテキスト*します。 したがって、システム アカウントはグローバルに実行されます。 **\dosdevices\z**コンテキスト。

スレッドは、ローカルで実行されている場合**\dosdevices\z**コンテキスト、ローカルでのみ、作成した MS-DOS デバイス名が作成されます**\dosdevices\z**ディレクトリ。 そのため、ローカルで実行されているスレッド**\dosdevices\z** MS-DOS デバイス名のローカルで実行されているスレッドに表示されることはできませんコンテキストの影響を与える**\dosdevices\z**コンテキストまたはグローバル**\Dosdevices\z**コンテキスト。 たとえば、ユーザーが Windows XP またはそれ以降のマウントの場合、ネットワーク ドライブとして**x:**、これの意味は影響しません**x:** 他のユーザーまたはシステム全体として。

Windows xp 以降に、内の名前とオブジェクト manager は **\\\dosdevices\z**、最初に、ローカル検索 **\\\dosdevices\z**ディレクトリ、および、グローバル **\\\Dosdevices\z**ディレクトリ。 両方の場所で名前が存在する場合、ローカル名はグローバルの名前をシャドウします。

Windows 2000 では、新しいターミナル サーバー セッションが開始されるたびに、システムを構築ローカル\\ **\dosdevices\z**ディレクトリ、グローバルにコピーして **\\\dosdevices\z**ディレクトリ。 それ以降の変更をグローバル ディレクトリには、ローカル ディレクトリには反映されません。

グローバルで、MS-DOS デバイス名を作成する必要がありますドライバー  **\\\dosdevices\z** など、システムのスレッドコンテキストで実行することが保証される標準のドライバーのルーチンでそのシンボリックリンクを作成して実行できますディレクトリ**DriverEntry**します。 または、グローバル **\\\dosdevices\z**ディレクトリは **\\\dosdevices\z\\Global**; ドライバーの名前を使用できます、  **\\\Dosdevices\z\\Global\\**<em>DosDeviceName</em>グローバル ディレクトリの名前を指定します。

なお **\\\dosdevices\z\\Global** local と global のバージョンをサポートしていないプラットフォームに存在しない **\\\dosdevices\z**、Windows 98 など/me. 次のコード例は、Windows 98 で動作するグローバルのシンボリック リンクを作成します]、[自分だけでなく Windows 2000 以降のオペレーティング システム。

```cpp
UNICODE_STRING deviceName; // Already initialized.
UNICODE_STRING symbolicLinkName; // Initializing below.
NTSTATUS status;

if (IoIsWdmVersionAvailable(1, 0x10)) {
    // We're on Windows 2000 or later, so we use \DosDevices\Global.
 
    RtlInitUnicodeString(&symbolicLinkName, L"\\DosDevices\\Global\\SymbolicLinkName");

} else {
    // Windows 98/Me.  We just use DosDevices.
 
    RtlInitUnicodeString(&symbolicLinkName, L"\\DosDevices\\SymbolicLinkName");
}

status = IoCreateSymbolicLink(&symbolicLinkName, &deviceName);
if (!NT_SUCCESS(status)) {
  /* Symbolic link creation failed.  Handle error appropriately. */
}
```

ドライバーは、ローカルの MS-DOS デバイス名を作成できます **\\\dosdevices\z** IOCTL への応答にシンボリック リンクを作成してディレクトリ。 ときに特定のローカル スレッド**\dosdevices\z**コンテキストから送信される、IOCTL、ドライバーの*DispatchDeviceControl*から現在のスレッドのコンテキスト内で呼び出されます。

標準のドライバーのルーチンが実行されるコンテキストに関する詳細については、次を参照してください。[ディスパッチ ルーチンは、Irql](dispatch-routines-and-irqls.md)します。

ローカル システムを区別 **\\\dosdevices\z**ディレクトリとして次のとおりです。

-   Windows xp と以降では、ローカル **\\\dosdevices\z**ディレクトリがで識別される、 **AuthenticationID**ログオン セッションのアクセス トークン。 詳細については、 **AuthenticationID**の説明を参照して、**トークン\_統計**Microsoft Windows SDK ドキュメントの構造体。

-   Windows 2000 では、ローカルで **\\\dosdevices\z**ディレクトリがで識別される、 **SessionId**ターミナル サーバー セッションのです。 詳細については、 **SessionId**の説明を参照して、 **WTS\_セッション\_情報**Windows SDK ドキュメントの構造体。

Windows NT 4.0 Terminal Server Edition がサポートしているローカル\\ **\dosdevices\z** Windows 2000 とまったく同じ方法でディレクトリ。

 

 




