---
title: INF Reboot ディレクティブ
description: Reboot ディレクティブは、インストールの完了後にシステムを再起動するように呼び出し元に通知する必要があることを示します。
ms.assetid: 0E2640EA-921D-4677-82EF-EF9707254E66
keywords:
- INF 再起動ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Reboot Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bd09765ba9f3745bf9cb8c1114c0dfe60efa201
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223126"
---
# <a name="inf-reboot-directive"></a>INF Reboot ディレクティブ

**Reboot**ディレクティブは、インストールの完了後にシステムを再起動するように呼び出し元に通知する必要があることを示します。

```inf
[DDInstall]
  
Reboot
```

**警告**   **Reboot**ディレクティブは、 ** \[ddinstall\] **セクションで直接指定されている場合にのみ処理されます。

 

システムの再起動が必要になるのは、デバイスのインストールの一部として検出された一般的な条件に基づいて自動的に検出されるため、Windows でのインストールのために INF ファイルでは**reboot**ディレクティブがほとんど指定されていません。 たとえば、ファイルコピー操作の対象となるターゲットファイルが使用されている場合、またはインストール中にデバイスを自動的に再起動できない場合は、再起動が必要であることを呼び出し元に通知します。 **Reboot**ディレクティブは、システム自体によって自動的に検出されない、このドライバーのインストール後にシステムの再起動が常に必要になる特定の条件がある場合にのみ使用してください。

Reboot ディレクティブを指定すると、この INF インストールセクションを使用して、任意のデバイスのインストールを完了するためにシステムの再起動が必要であることが、呼び出し元に通知されます。 [**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)、 [**Diinstalldriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)、 [**diinstalldriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)などの関数によってインストールが開始されると、これらのルーチンの "*再起動*を必要とする" パラメーターが TRUE に設定されます。

<a name="remarks"></a>解説
-------

Windows 7 以前では、**再起動**ディレクティブが指定されたドライバーを使用してデバイスをインストールすると、インストールを完了するためにシステムの再起動が必要であることが、呼び出し元に通知されます。

Windows 8 以降では、インストールされる1つ以上のデバイスが既に開始されている場合にのみ、上記の動作が発生します。 新しいドライバのインストール中にデバイスを再起動するのではなく、システムの再起動が必要であることを呼び出し元に通知し、新しいドライバのインストールを完了する必要があります。 インストールするデバイスが現在開始されていない場合は、システムの再起動を必要とせずに、インストールの実行が試行されます。 ただし、インストールのいずれかの操作で必要になる場合は、再起動が必要になることに注意してください。 たとえば、コピーする一部のファイルのコピー先ファイルの場所が現在使用中の場合、インストールを完了するためにシステムの再起動が必要になります。

 

 





