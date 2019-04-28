---
title: フィルター マネージャー操作の制御
description: フィルター マネージャー操作の制御
ms.assetid: 884e6a15-5bfa-41bf-b759-af6e43078fad
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、操作を制御します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b87373d79ec8c9e5c99b85001a1d402040512b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370694"
---
# <a name="controlling-filter-manager-operation"></a>フィルター マネージャー操作の制御


Windows Vista は、REG によって制御されるより前のバージョンの Windows 上のフィルター マネージャーの操作\_DWORD *AttachWhenLoaded*レジストリ値が次のキーに格納されます。

```cpp
HKLM\System\CurrentControlSet\Services\FltMgr
```

ときに*AttachWhenLoaded*設定が 0 の場合にフィルター マネージャー アタッチできないのすべてのボリューム フィルター マネージャーとミニフィルター ドライバーに登録されるまで。 ときに*AttachWhenLoaded*フィルター マネージャー接続のすべてのボリュームのブート時に、1 に設定されます。

既定値*AttachWhenLoaded*は Windows XP Service Pack 2 (SP2) 以降では 0 です。

既定値*AttachWhenLoaded*は Windows Server 2003 Service Pack 1 (SP1) および以降のバージョンの 1。

*AttachWhenLoaded*レジストリ値は、Windows Vista に存在しないと、Windows の以前のバージョンにのみ適用されます。

ミニフィルター ドライバーは、Windows Vista より前の Windows にインストールするときにソフトウェアのインストーラーを設定する必要があります*AttachWhenLoaded*このレジストリ値が 1 に現在設定されていない場合は 1 にします。 場合の以前の値*AttachWhenLoaded*が 0 の場合、インストーラーはミニフィルター ドライバーのインストール後に、システムを再起動する必要があります。

 

 




