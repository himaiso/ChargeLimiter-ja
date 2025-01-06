##元の文章を翻訳したもののため、意味が変わっている可能性があります。

## はじめに

ChargeLimiter(CL)は、iDeviceが過充電になるのを防ぎ、バッテリーにダメージを与えるのを防ぐために使用されているMacOSのAlDenteにインスパイアされたものです。    

Rootful Jailbreak（arm.deb）/Rootless Jailbreak（arm64.deb）/TrollStore（.tipa）をサポートしています。
現在は、iOS12-17.0をサポートしています。（注意：TrollStoreを使用する場合は、新しいバージョンをインストールする前に古いバージョンのCLをアンインストールしてください）       

iPhone6/7+iOS12/13の Checkra1n/Unc0ver/Odysseyや、iPhone7/X/11+iOS15/16のPalera1n/Dopamine/TrollStoreで動作確認をしています。

v1.4.1はほとんどのユーザーを使用している方向け。v1.5はChargeInhibitをサポートしていないバッテリーを使用している方向け。v1.6は充電中のアンペア数が大きすぎるバッテリーを使用している方向け。 

このプロジェクトはオープンソースです。より良いアイデアがあれば、コードを送信してください。意見があれば、issueを追加してください。
このソフトウェアはオープンソースで、広告なしで無料です。このソフトウェアが原因でiOSシステムやハードウェアに影響が生じた場合、著者は一切の責任を負いません。   

![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/banner.jpg)

## 既知の問題

* テスト用のデバイスが不足しているため、CLはiOS<=11ではサポートされない可能性があります。
* iOS<=12ではフローティングウィンドウはサポートされていません。
* deb 版では、一部の調整により CL が SplashScreen で停止することがありますが、これは CL 自体のバグではありません。com.apple.UIKit に注入されたこれらの調整は、/Library/MobileSubstrate/DynamicLibraries(rootful) および /var/jb/Library/MobileSubstrate/DynamicLibraries(rootless) にあります。

## FAQ

CLを使用する理由は？
* iDeviceは常に電源に接続されている
* iDeviceは常に一晩充電されている
* 充電中の温度を管理したい

CLはより多くの電力を消費しますか？
* ほとんどのユーザーにとっては影響がありません。 アプリのUIとフローティングウィンドウが1秒間隔で更新されている場合、若干の電力が消費される可能性があります。 もしバッテリー残量が急速に減少していると感じる場合は、更新間隔を1分に設定してみてください。

CLはサードパーティ製バッテリーをサポートしていますか？
* CLはほとんどのブランドのバッテリーをサポートしています。

CLを一定期間使用すると、バッテリー残量パーセントが増加しますか？
* 特にソフトウェアではありえないと思いますが、CLを1か月間使用した後にバッテリー残量が増えたというユーザーも実際にいます。
* CLはほとんどのユーザーのバッテリー残量低下速度を遅くします。
* ヘルスパーセンテージは一定の範囲で変動する可能性があります。CLを使用した後もヘルスパーセンテージが低下し続けるユーザーはほとんどいません。この場合はCLの使用を中止してください。
* 電源に接続し続け、ChargeInhibit（DisableInflowなし）を可能な限り有効にしておくと、通常のアンペア数は0mAとなり、バッテリーのヘルスパーセンテージは低下しません。

なぜ私のiDeviceは充電または放電できないのですか？（初心者からの質問で最も多いもの）
CLは完全自動のツールではありません。温度制御が有効になっている場合は、実際の温度に応じて閾値を慎重に設定してください。そうしないと、CLは確実に充電を停止し、それ以上再充電を行いません。
CLは充電回数を最小限に抑えるように設計されています。そのため、「プラグアンドチャージ」モードで電源に接続しても充電を開始したり充電を回復したりせず、電源に再接続すると充電を開始します。
* 状態の悪いバッテリーでは、ChargeInhibit/DisableInflowが正常に動作しない場合があります。この場合、システムを再起動すると正常に動作しますが、数十分後にはまた動作しなくなります。CLは、この種のバッテリーでは使用できません。状態の悪いバッテリーで動作不良が起こるケースは、ごく一部です。
過熱したバッテリーは、ChargeInhibitの障害を引き起こす可能性があります。この場合、バッテリーが冷えると正常に復帰します。過熱したバッテリーすべてに障害が発生するわけではありませんのでご注意ください。
* アクティベーションされていない新しいバッテリーは、5mAをはるかに超える電流を引き起こす可能性があり、完全なChargeInhibitを破損します。
* iPadの場合、バッテリーが正常に充電され、容量が増えない場合、電源の説明が「pd charger」と表示されている場合は、ケーブルを差し直したり、ケーブルや充電器をより良いものに交換したりしてみてください。

脱獄やTrollStoreのような環境がなくてもCLをインストールすることは可能ですか？
* CLではプライベートAPIを使用しているため、App Storeで公開することはできません。
* CLでは特別なエンタイトルメントを使用しているため、一般的なipaファイルとしてインストールすることはできません。

夏場のバッテリー冷却方法
CLに搭載されている「Powercuff」機能でiDeviceハードウェアの消費電力を抑えることで、充電時のワット数を減らすことができます。
充電にはワット数の低い充電器を使用します。
放熱機能付きのものを使用します。

バッテリーを健康に保つ最善の方法は？
* <https://www.apple.com.cn/batteries/maximizing-performance/>を参照してください
* 極端に高温または低温の環境での使用は避けてください
* 長時間の過充電は避けてください
* 電源が切れた状態は避けてください

何か問題が発生した場合、CLを自分でデバッグするにはどうすればよいですか？
* 5分チャートとログ（/var/root/aldente.log）のデータを表示して、充電/放電の履歴データを検証します。

CLでパワーキラーアプリを見つけるにはどうすればよいですか？
* アプリを開くか、システム機能を有効にしてしばらく待ち、5分チャートまたはHeliumアプリのアンペア数でデータを表示して、キラーを見つけます。

## 互換性

CLを使用する前にバッテリーの互換性をテストしてください。サポートされていない場合は、CLを停止し、アンインストールしてください
* 1.ChargeInhibitの互換性を確認してください。まず「有効」ボタンを切り替えてCLを無効にし、「詳細設定」内のすべてのオプションを無効にします。次に「充電」ボタンを切り替えて充電を無効にします。120秒以内に何か変化があれば、ChargeInhibitがサポートされていることを意味します。ただし、無効にした後もInstantAmperageが5mA以上を維持している場合はこの限りではありません。（InstantAmperageは、一部の種類のバッテリーでは無効になる場合があります。この場合、容量の増加を確認してください。）
* 2.PredictiveChargingInhibitの互換性を確認してください。「Advanced-Predictive charging inhibit」から有効にし、その後「1」の手順に従ってください。
* 3.DisableInflowの互換性を確認してください。Enableボタンを切り替えてCLを無効にし、有効になったら「External connected」ボタンを切り替えて流入を無効にします。120秒以内に何か変化があれば、DisableInflowがサポートされていることになります。ただし、無効にした後もInstantAmperageが5mA以上を維持している場合はこの限りではありません（InstantAmperageは、一部の種類のバッテリーでは無効になる場合があります。この場合は、容量増加を確認してください）。
* 状態の良くないバッテリーでは、CLが正常に動作しない場合があります。この場合、システムを再起動するとCLは正常に充放電を制御できますが、数十分後には制御できなくなります。この種のバッテリーではCLは使用できません。
* ChargeInhibitもDisableInflowもサポートされていない場合、バッテリーはCLでサポートされることはありません。
CLを使用中にバッテリーの健康状態が異常に低下し続ける場合は、アドバンスメニューで設定を調整するか、CLをアンインストールしてください。

## バッテリーの起動

公式文書：<https://www.apple.com.cn/batteries/maximizing-performance/>

## バッテリーバンクとの互換性

CLはモバイルバッテリーと併用できます。iDeviceは、まずChargeInhibitモードでモバイルバッテリーから給電され、モバイルバッテリーが切れた後にiDeviceのバッテリーから給電されます。これは、長距離の移動を予定しているユーザーにとって有益です。モバイルバッテリーは、バッテリーよりも容量が大きく、価格も安いです。注意：
ワイヤレス充電のワット数が不十分な場合、バッテリーが同時に電力を供給することがあります。充電器が供給できる以上の電力を携帯電話自体が消費する場合は、ワイヤレス充電器を使用することは適していません。
* ほとんどの有線式モバイルバッテリーは「スリープモード」をサポートしており、一定時間電流が一定の閾値を下回ると、モバイルバッテリーは自動的に電源をオフにします。このモードでCLを使用している場合、携帯電話がロックされた後に電流が低くなり、モバイルバッテリーが電源をオフにすることがあります。この場合、電源が切断されるため、CLはそれ以上充電することができません。
ほとんどの有線式モバイルバッテリーは、電源ボタンをダブルクリックするか長押しすることで「低電流モード」をサポートしており、電流が少なくなった場合でもモバイルバッテリーが自動的に電源をオフにすることはありません。このモードでは、画面がロックされた後もCLは正常に動作します。ただし、一部のモバイルバッテリーは数時間後に自動的に「低電流モード」を終了しますのでご注意ください。

## 注意

* iPhone8+(またはそれ以上)の場合、充電状態の設定後、120秒の遅延があります。iPadも同様かもしれません。
* ChargeInhibitモードでは、システムステータスバーのライトニングアイコンは更新されず、実際の充電状況は3utools（および類似品）またはCLで確認できます。一方、DisableInflowモード（iPhone8+）では更新されます。このモードは「Advanced-Control inflow」で有効になります。
TrollStoreの場合、CLのデーモンが何らかの理由で終了した場合（システム再起動、ユーザースペース再起動など）、CLは自動的にデーモンを再起動できないため、無効になります。
CLは充電回数を最小限に抑えるように設計されているため、「プラグアンドチャージ」モードで電源に接続しても充電を開始または回復することはありません。充電は、後述の特定の条件下でのみ開始または停止します。
CLは、設定.appの「最適化バッテリー充電」と互換性がありません。必要に応じて、CLを無効にした後、設定.appで再度有効にしてください。最新のiDeviceでCLを使用することは推奨されません。「最適化バッテリー充電」はiPhone15からすでに完璧です。
* iDeviceがChargeInhibitモードに長時間留まっていると、ハードウェア統計が不正確になる可能性があります。少なくとも月に一度はバッテリーの充電/放電を行うことをお勧めします。

## 説明

### 条件

* ChargeInhibit: バッテリーへの電流の流れを禁止します。このモードではバッテリーは充電も放電も行わず、電源がiDeviceのハードウェアに直接電力を供給します。このモードが優先されるべきです。
* DisableInflow: iDevice への電流の流れを禁止します。このモードではバッテリーが放電し、iDevice のハードウェアに電源が供給されます。このモードは、ChargeInhibit がバッテリーによってサポートされていない場合にのみ使用してください。
* LimitInflow: 電流を制限し、iDevice の過熱を防止します。このモードは、バッテリーが電流を制御できない場合にのみ使用してください。

### 「有効」ボタン

CLをグローバルに有効または無効にします。無効にするとCLは読み取り専用のオブザーバとなり、バッテリー情報のみを表示します。

### フローティングウィンドウ

* バッテリー情報とデーモンの状態をリアルタイムで表示
* ドラッグして任意の場所に移動できます。
* タップするとCLをグローバルに有効または無効にできます。「有効」ボタンと同じです。
* 「自動的に隠す」が有効になっている場合、他のアプリが前面にあるときは自身を隠します。

### モード

「プラグアンドチャージ」モードは個人向けで、いつでも充電と放電が可能です。トリガーは以下の通りです。
* USBケーブルを差し直すと、条件が満たされていれば充電を開始します。
* 現在の容量が指定値より低ければ充電を開始します。
* 現在の容量が指定値より高ければ充電を停止します。
* 温度が指定値より低ければ充電を開始します。
* 温度が指定値より高ければ充電を停止します。

「エッジトリガー」モードは、常に電源に接続されているiDevice用の開発者およびスタジオ向けモードで、以下のトリガーを使用します。
* 現在の容量が指定値より低い場合、充電を開始します。
* 現在の容量が指定値より高い場合、充電を停止します。
* 温度が指定値より高い場合、充電を停止します。

優先順位の高いものから低いものへとトリガーされます。
* 充電開始（極端に容量が低い場合） 
* 充電停止（容量＞温度）
* 充電開始（容量＞温度＞プラグイン）

### 更新頻度

* 更新頻度は、UIのデータ更新速度です。アプリUIとフローティングウィンドウの両方です。
* 更新頻度が低いほど、より多くの電力を節約できる可能性があります。ほとんどのユーザーは1秒で問題ありませんが、お好みで設定してください。

### しきい値

* デフォルトの閾値は20/80/10/35に設定されています。CLを期待通りに動作させるには、ご自身で調整する必要があります。
* 温度のしきい値は「履歴-時間ごとのデータ」に従って設定してください。
* トリガーで停止する実際の値は、必ずしも目標値と一致するとは限りません。ほとんどの状況では、その差は0～1%ですが、一部のユーザーでは3～5%の差が生じています。この差は、「120秒の遅延」、充電速度、およびバッテリーハードウェア自体と何らかの関係があります。充電停止後に弱いアンペアが発生した場合、その差は3%より高くなるかもしれません。また、バッテリーの状態が突然変化した場合にも、このような状況が発生する可能性があります。活性化されていない新しいバッテリーの場合にも、このような状況が発生する可能性があります。

### アクション

充電の開始/停止のトリガーに対するアクション。CLを再インストール/更新した後は、リセットしてください。

### 詳細

* 「スマートバッテリー」と「予測充電抑制」については、ほとんどのユーザーにとってデフォルト設定が最適です。 これらを再設定して、最適な設定を見つけてください。
* 「流入自動抑制」と「DisableInflow」モードは、ChargeInhibitモードをサポートしていないバッテリー用です。有効にすると、充電を停止した後にiDeviceがバッテリーの電力を消費し始めます。
* 熱シミュレーション、Powercuffと同じで、温度が高ければ高いほど、ハードウェア（充電器/CPU/GPU/バックライト/WiFi/ラジオ/スピーカー/アークなど）の消費電力は少なくなり、パフォーマンスは低下し、充電電流と充電電圧は低下します。iOSシステム自体が実際の状況に応じてステータスを更新します。特定の値を強制的に変更したい場合は（推奨しません）、「ロック」を有効にしてください。CLは、脱獄環境下で同様の機能を持つ他のTweakと競合した場合、無効になります。
* ピークパワー：低温または低容量時のピークパワー性能を制御します。変更する場合は、何を変更するのかを理解している場合のみ行ってください。
* 自動流入制限、高温およびバッテリーの健康状態低下によるアンペア数の制御不能に対して、熱シミュレーションを適用します。この方法で不安定なレベルを見つけることができます。電流容量が30%以下になったら充電を開始します（容量が低いほど、アンペア数は高くなります）。「高度な-熱シミュレーション」レベルを選択します（「標準」から「重い」まで、レベルが高いほどアンペア数は低くなります）。アンペア数は数秒で変化します。許容できるアンペア値が見つかったら、レベルを「高度-自動流入制限-熱シミュレーション」に設定します。この場合、CLが充電を開始すると、熱シミュレーションレベルは「高度-自動流入制限-熱シミュレーション」で指定したレベルに自動的に設定され、CLが充電を停止すると、デフォルトのレベルである「高度-熱シミュレーション」に設定されます。

### バッテリー情報

バッテリーの健康度は NominalChargeCapacity で計算されます。一般的に、新品のバッテリーの健康度は100%を超えており、システムステータスバーでは常に100%と表示されます。長期間のChargeInhibitにより、健康度が突然大幅に低下する可能性があることに注意してください。この場合、CLを一時的に無効にして、バッテリーを完全に充電する操作を数回繰り返して健康度を回復させる必要があります。
ハードウェア容量はシステム容量に近く、ほとんどの場合、より正確です。違いが大きすぎる場合は、バッテリーが較正されていないか、品質が悪いことを示している可能性があります。過充電の場合は、ハードウェア容量が100% (システムステータスバーでは100%) を超える可能性があり、過放電の場合は、マイナス (システムステータスバーでは0) になる可能性があります。
* InstantAmperage が正の値の場合は電源からバッテリーへの電流の流れを意味し、負の場合は電源のないバッテリーから iDevice への電流の流れを意味します。InstantAmperage は通常、ChargeInhibit モードでは 0mA であるべきで、この場合、電流はバッテリーを通って iDevice に流れます。バッテリーを直接電源として使用するよりもバッテリーへのダメージは少なくなります。（*実際には、電源に接続し続け、充電を停止すると、バッテリー寿命が低下することはありません*）。InstantAmperageは、DisableInflowモードでは負の値になります。

### 履歴

&emsp;&emsp;一定期間のバッテリーの状態を表示します。時間を変更するには水平にスライドさせ、凡例をクリックして特定のソースを隠したり表示したりします。

* 5分間隔のデータ、電流容量/温度/電流を含む、各充電または放電サイクルの詳細なバッテリー状態を表示します。
* 1時間間隔のデータ、電流容量/温度/電流を含む、すべての充電または放電サイクルのバッテリー状態を表示します。
* 1日ごとのデータ、各日のバッテリー状態を詳細に表示します。
* 1か月ごとのデータ、各月のバッテリー状態を表示します。

### For Shortcuts.app

新規ショートカット - アクションを追加 - Web - Safari - URLを開く 
* cl:/// (CLを開く)
* cl:///exit (CLを開き、CLを終了し、デーモンを起動する)
* cl:///charge (CLを開き、充電を開始する)
* cl:///charge/exit (CLを開き、充電を開始し、CLを終了する)
* cl:///nocharge (CLを開き、充電を停止する)
* cl:///nocharge/exit (CLを開き、充電を停止し、CLを終了)

統合ショートカット（iOS16+）： <https://www.icloud.com/shortcuts/2ec3aed94f414378918f3e082b7bf6b0>

### HTTPインターフェース

* 例

```bash
curl http://localhost:1230 -d '{「api」:「get_conf」,「key」:「enable」}' -H 「content-type:application/json」
=> {」status「:0,」data":true}
```

* グローバル設定フィールド

|key                                         |type         |description                                                                               |
|----------------------------------|-----------|---------------------------------------------------------------------|
|enable                                     |boolean         |CL will become an readonly observer if disabled, and shows battery information only|
|floatwnd                                  |boolean         |Floating window                                                                      |
|floatwnd_auto                         |boolean         |Floating window auto hide                                                      |
|mode                                       |string     |Mode,"charge_on_plug" or "edge_trigger"                             |
|charge_below                         |integer         |Capacity threshold                                                                |
|charge_above                         |integer         |Capacity threshold                                                               |
|enable_temp                           |boolean         |Temperature control                                                               |
|charge_temp_above               |integer         |Temperature threshold                                                         |
|charge_temp_below               |integer         |Temperature threshold                                                         |
|acc_charge                             |boolean         |Speedup charging                                                                 |
|acc_charge_airmode              |boolean         |Airplane mode                                                                       |
|acc_charge_wifi                      |boolean         |WiFi                                                                                       |
|acc_charge_blue                    |boolean         |Bluetooth                                                                               |
|acc_charge_bright                  |boolean         |Brightness                                                                             |
|acc_charge_lpm                     |boolean         |LPM                                                                                       |
|action                                     |string      |Action on trigger, "noti" to use system notification              |
|adv_prefer_smart                   |boolean         |Use SmartBattery                                                                  |
|adv_predictive_inhibit_charge|boolean         |Use predictive inhibit charge                                                |
|adv_disable_inflow                 |boolean         |Auto inhibit inflow                                                                 |
|adv_limit_inflow                     |boolean         |Auto limit inflow                                                                     |
|adv_limit_inflow_mode          |string      |Auto limit inflow with thermal simulation level,off/nominal/light/moderate/heavy|
|adv_def_thermal_mode         |string      |Default thermal simulation level,off/nominal/light/moderate/heavy|
|adv_thermal_mode_lock        |boolean         |Lock thermal simulation level                                               |
|thermal_simulate_mode         |string     |Actual  thermal simulation level(readonly)                            |
|ppm_simulate_mode             |string      |Actual Peak power performance level                                 |
|use_smart                              |boolean         |SmartBattery available(readonly)                                          |

* get_conf

|request     |type        |description                           |
|------------|-----------|--------------------------------|
|api            |string      |get_conf                               |
|key            |string     |return all conf if unspecified|
|response  |                |                                            |
|status       |integer    |0:success                            |
|data         |                |data                                     |

* set_conf

|request     |type        |description                           |
|------------|-----------|--------------------------------|
|api            |string    |set_conf                               |
|key            |string    |Global configuration fields  |
|val            |               |data                                     |
|response         |                |                                            |
|status       |integer        |0:success                        |
|data         |                |data                                   |

* get_bat_info

|request     |type        |description                           |
|------------|-----------|--------------------------------|
|api            |string    |get_bat_info                         |
|response         |                |                                            |
|status       |integer        |0:成功                                  |
|data         |                |数据                                     |

|key                                     |type         |description                           |
|-------------------------------|-----------|--------------------------------|
|Amperage                           |integer        |(mA)                                 |
|AppleRawCurrentCapacity |integer        |(mAh)                               |
|BatteryInstalled                   |boolean        |(mV)                               |
|BootVoltage                        |integer        |(mV)                                 |
|CurrentCapacity                 |integer        |(%)                                   |
|CycleCount                        |integer        |                                         |
|DesignCapacity                  |integer        |(mAh)                               |
|ExternalChargeCapable     |boolean        |                                      |
|ExternalConnected            |boolean        |                                      |
|InstantAmperage                |integer        |(mA)                                |
|IsCharging                          |boolean        |                                      |
|NominalChargeCapacity    |integer        |(mAh)                              |
|Serial                                  |string          |                                        |
|Temperature                       |integer        |(℃/100)                          |
|UpdateTime                       |integer        |                                        |
|AdapterDetails.Voltage      |integer        |(mV)                                |
|AdapterDetails.Current      |integer        |(mA)                               |
|AdapterDetails.Description|integer        |                                      |
|AdapterDetails.IsWireless  |integer        |                                      |
|AdapterDetails.Manufacturer|integer     |                                     |
|AdapterDetails.Name         |integer        |                                     |
|AdapterDetails.Voltage      |integer        |(mV)                               |
|AdapterDetails.Watts         |integer        |(W)                                 |

* set_charge_status

|request         |type         |description                                    |
|------------|-----------|-------------------------------|
|api            |string    |set_charge_status               |
|flag          |boolean         |enable                                     |
|response         |                |                                            |
|status       |integer        |0:success                                  |

* set_inflow_status

|request         |type         |description                                    |
|------------|-----------|-------------------------------|
|api            |string    |set_inflow_status                |
|flag          |boolean         |enable                                     |
|response         |                |                                            |
|status       |integer        |0:success                                  |

より良いアイデアをお持ちの方は、ぜひプロジェクトに参加してコードをプッシュしてください。
ダウンロードURL: (https://github.com/lich4/ChargeLimiter/releases) 
Telegramグループ: ![](https://img.shields.io/static/v1?label=&message=https://t.me/chargelimiter&color=red) 
https://t.me/chargelimiter

![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en0.png)
![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en1.png)
![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en2.png)
![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en3.png)
![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en_stat0.png)
![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en_stat1.png)
![](https://raw.githubusercontent.com/lich4/ChargeLimiter/main/screenshots/screenshots_en_night.png)


### コンパイル

XCode+MonkeyDev または Theos
* XCode を使用してアプリをデバッグします。https://github.com/lich4/debugserver_azj を参照してください。
* WebUI をデバッグします。https://github.com/lich4/inspectorplus を参照してください。
* TrollStore にインストールします。https://github.com/lich4/TrollStoreRemoteHelper を参照してください。

新しい言語を追加： `www/lang.json` `www/help_en.md` を修正し、githubまたは私に提出してください。

## 特別感謝

* アイコン：Elfulanopr
* 繁体字中国語：Olivertzeng
* アラビア語：Nawaf
* ベトナム語：Trickbox0411 
* ダークモード：InnovatorPrime 
* ショートカット：Cast
* 日本語：@himais0
