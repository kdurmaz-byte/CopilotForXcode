# Herhangi Bir Cihazdan Yerel Oturumları Remote Control ile Devam Ettirin

> Remote Control, claude.ai/code veya Claude mobil uygulamasını yerel olarak çalışan bir Claude Code oturumuna bağlar. Masaüstünüzde bir görev başlayın, ardından telefonunuzda veya başka bir bilgisayarda devam edin.

<Note>
  Remote Control araştırma önizlemesindedir ve tüm planlarda mevcuttur. Team ve Enterprise'da, varsayılan olarak Remote Control oturumları kapalıdır — bir Sahip, [Claude Code yönetici ayarlarında](https://claude.ai/admin-settings/claude-code) Remote Control geçişini etkinleştirene kadar.
</Note>

Remote Control, [claude.ai/code](https://claude.ai/code) veya [iOS](https://apps.apple.com/us/app/claude-by-anthropic/id6473753684) ve [Android](https://play.google.com/store/apps/details?id=com.anthropic.claude) için Claude uygulamasını, makinenizde çalışan bir Claude Code oturumuna bağlar. Masaüstünüzde bir görev başlayın, ardından telefonunuzda kanepede veya başka bir bilgisayarda devam edin.

Remote Control oturumu başlattığınızda, Claude yerel olarak çalışmaya devam eder, bu nedenle kod yürütme ve dosya sistemi erişimi makinenizde kalır. Remote Control ile şunları yapabilirsiniz:

* **Tam yerel ortamınızı uzaktan kullanın**: dosya sisteminiz, [MCP sunucuları](/docs/en/mcp), araçları ve proje yapılandırması tümü mevcuttur ve `@` yazarak yerel projenizin dosya yollarını otomatik tamamlayabilirsiniz.
* **Her iki yüzeyden de çalışın**: konuşma ve [alt ajanlar](/docs/en/sub-agents) ile [dinamik iş akışlarının](/docs/en/workflows) ilerleme durumu bağlı tüm cihazlarda senkronize kalır, böylece terminal, tarayıcı ve telefon arasından indistinktif olarak ileti gönderebilirsiniz.
* **Telefonunuzdan veya tarayıcıdan görüntü ve dosya gönderin**: Claude uygulamasına veya claude.ai/code'a bir fotoğraf veya dosya ekleyin, resim yazılı olsun veya olmasın. Claude ekli fotoğrafları doğrudan mesajınızın bir parçası olarak görmek ve dosyaları makinenize indirebilir; Claude Code onları `@` dosya referansları olarak iletir.
* **Kesintilerin üstesinden gelin**: Dizüstü bilgisayarınız uyku moduna geçerse veya ağ bağlantınız kesilirse, makineniz tekrar çevrimiçi olduğunda Claude Code otomatik olarak yeniden bağlanır. Claude Code alt ajanları ve iş akışlarından gelen durum güncellemelerini bağlantı yeniden kurulurken kuyruğa alır ve kurtarıldıktan sonra teslim eder.

[Claude Code web'deki](/docs/en/claude-code-on-the-web) aksine, bulut altyapısında çalışan Remote Control oturumları makinenizde doğrudan çalışır ve yerel dosya sisteminizle etkileşime girer. Web ve mobil arayüzler bu yerel oturuma bir penceredir.

Bu sayfa kurulumu, oturumları başlatma ve bağlama ve Remote Control'ün Claude Code web'de nasıl karşılaştırıldığını kapsar.

## Gereksinimler

Remote Control'ü kullanmadan önce, ortamınızın bu koşulları karşıladığını doğrulayın:

* **Abonelik**: Pro, Max, Team ve Enterprise planlarında mevcuttur. API anahtarları desteklenmez. Team ve Enterprise'da, bir Sahip önce [Claude Code yönetici ayarlarında](https://claude.ai/admin-settings/claude-code) Remote Control geçişini etkinleştirmelidir.
* **Kimlik Doğrulama**: `claude` çalıştırın ve henüz yapılmadıysa claude.ai aracılığıyla oturum açmak için `/login` komutunu kullanın. Uygun bir oturum açma olmadan, `claude remote-control` bir hata ile çıkar, `claude --remote-control` yine de interaktif bir oturum başlatır ve yakında bir Remote Control başarısızlık bildirimi gösterir.
* **API uç noktası**: Amazon Bedrock, Google Cloud'ın Agent Platform veya Microsoft Foundry'de kullanılamaz. v2.1.196 itibariyle, [`ANTHROPIC_BASE_URL`](/docs/en/env-vars) `api.anthropic.com` dışında bir ana bilgisayara işaret ettiğinde Remote Control devre dışı bırakılır (örn. [LLM ağ geçidi](/docs/en/llm-gateway) veya proxy gibi). Remote Control'ü kullanmak için değişkeni ayarlanmamış olarak bırakın.
* **Özellik bayrağı değerlendirmesi**: [`DISABLE_TELEMETRY`, `DO_NOT_TRACK`, `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` ve `DISABLE_GROWTHBOOK`](/docs/en/env-vars) her biri, Remote Control kullanılabilirliğinin bağlı olduğu özellik bayrağı değerlendirmesini devre dışı bırakır. Remote Control'ü kullanmak için değişkeni, kabuğu ortamında veya [`settings.json`](/docs/en/settings#available-settings) dosyasının `env` bloğunda ayarlı olduğu yerde ayarlanmamış olarak bırakın.
* **Çalışma alanı güveni**: proje dizininizde en az bir kez `claude` çalıştırarak çalışma alanı güveni diyalogunu kabul edin. Başlangıç güveni diyaloğu hiçbir zaman ev dizinini kaydetmez, bu nedenle Remote Control'ü bir proje dizininden başlatın.

## Remote Control Oturumu Başlatın

CLI veya VS Code uzantısından Remote Control oturumu başlatabilirsiniz. CLI üç çağrı modu sunar; VS Code `/remote-control` komutunu kullanır.

<Tabs>
  <Tab title="Sunucu Modu">
    Proje dizininize gidin ve çalıştırın:

    ```bash theme={null}
    claude remote-control
    ```

    Süreç uzak bağlantıları bekleyerek sunucu modunda terminalinizde çalışmaya devam eder. Başka bir cihazdan [bağlanmak için](#connect-from-another-device) kullanabileceğiniz bir oturum URL'si görüntüler ve telefonunuzdan hızlı erişim için bir QR kodu göstermek için spacebar tuşuna basabilirsiniz. Uzak bir oturum etkinken, terminal bağlantı durumunu ve araç etkinliğini gösterir.

    Kullanılabilir bayraklar:

    | Bayrak                                            | Açıklama                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
    | ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `--name "Projelerim"`                           | claude.ai/code oturum listesinde görünen özel oturum başlığı ayarla.                                                                                                                                                                                                                                                                                                                                                                                                                          |
    | `--remote-control-session-name-prefix <prefix>` | Açık ad ayarlanmadığında otomatik oluşturulan oturum adları için ön ek. Makinenizin ana bilgisayar adında varsayılan, `myhost-graceful-unicorn` gibi adlar oluşturur. Aynı efekt için `CLAUDE_REMOTE_CONTROL_SESSION_NAME_PREFIX` ayarlayın.                                                                                                                                                                                                                                                    |
    | `-c`, `--continue`                              | Bu dizinde sunucunun son başlattığı oturumu geri getirin, bunun yerine yeni bir tane oluşturmak yerine. Bkz. [Sunucuyu durdurup Oturumları Yeniden Başlatın](#resume-sessions-after-stopping-the-server). `--session-id`, `--spawn`, `--capacity` veya `--create-session-in-dir` ile birleştirilemez. Claude Code v2.1.200 veya sonraki sürümleri gerektirir; eski sürümler bayrağı bilinmeyen bir argüman olarak reddeder.                                                                                                                            |
    | `--session-id <id>`                             | Oturum kimliğine göre bir oturumu geri getirin. Bkz. [Sunucuyu durdurup Oturumları Yeniden Başlatın](#resume-sessions-after-stopping-the-server). `--continue`, `--spawn`, `--capacity` veya `--create-session-in-dir` ile birleştirilemez. Claude Code v2.1.200 veya sonraki sürümleri gerektirir; eski sürümler bayrağı bilinmeyen bir argüman olarak reddeder.                                                                                                                                                        |
    | `--spawn <mode>`                                | Sunucunun oturumları nasıl oluşturduğu.<br />• `same-dir` (varsayılan): tüm oturumlar geçerli çalışma dizinini paylaşır, bu nedenle aynı dosyaları düzenlerken çakışabilir.<br />• `worktree`: talep üzerine her oturum kendi [git worktree](/docs/en/worktrees)'ini alır. Bir git deposu gerektirir.<br />• `session`: tek oturum modu. Tam olarak bir oturuma hizmet verir ve ek bağlantıları reddeder. Başlangıçta ayarlayın.<br />`same-dir` ve `worktree` arasında geçiş yapmak için çalışma zamanında `w` tuşuna basın. |
    | `--capacity <N>`                                | Maksimum eş zamanlı oturum sayısı. Varsayılan 32'dir. `--spawn=session` ile kullanılamaz.                                                                                                                                                                                                                                                                                                                                                                                                       |
    | `--[no-]create-session-in-dir`                  | Sunucu başladığında geçerli dizinde bir oturum önceden oluşturun, böylece yazacak yere sahip olun. `worktree` modunda bu oturum geçerli dizinde kalırken talep üzerine oluşturulan oturumlar izole edilmiş worktree'ler alır. Varsayılan olarak açık. Başlamak için hiçbirini olmayan `--no-create-session-in-dir` geçerseniz, Claude Code sunucuyu durdurduğunuzda oturumları arşivler, bu nedenle [yeniden başlatacak](#resume-sessions-after-stopping-the-server) bir şey yoktur.            |
    | `--verbose`                                     | Ayrıntılı bağlantı ve oturum günlüklerini göster.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
    | `--sandbox` / `--no-sandbox`                    | [Sandboxing](/docs/en/sandboxing)'i dosya sistemi ve ağ yalıtımı için etkinleştirin veya devre dışı bırakın. Varsayılan olarak kapalı.                                                                                                                                                                                                                                                                                                                                                                                                                  |

    Claude Code, Remote Control uygunluğunu yazdırmadan önce kontrol eder, bu nedenle `claude remote-control --help`, uygun bir hesapla oturum açmadığınızda bir hata döndürür.
  </Tab>

  <Tab title="İnteraktif Oturum">
    Remote Control etkinleştirilmiş normal interaktif bir Claude Code oturumu başlatmak için `--remote-control` bayrağını (veya `--rc`) kullanın:

    ```bash theme={null}
    claude --remote-control
    ```

    İsteğe bağlı olarak oturum için bir ad geçirin:

    ```bash theme={null}
    claude --remote-control "Projelerim"
    ```

    Bu size oturum başlatan bir tam interaktif oturum sağlar, ancak oturum da uzaktan claude.ai veya Claude uygulamasından kontrol edilebilir. `claude remote-control` (sunucu modu) aksine, yerel olarak ileti yazabilir ve oturum da uzaktan mevcuttur.
  </Tab>

  <Tab title="Mevcut Oturumdan">
    Zaten bir Claude Code oturumundasınız ve onu uzaktan devam ettirmek istiyorsanız, `/remote-control` (veya `/rc`) komutunu kullanın:

    ```text theme={null}
    /remote-control
    ```

    Özel oturum başlığı ayarlamak için bir ad argümanı geçirin:

    ```text theme={null}
    /remote-control Projelerim
    ```

    Bu, geçerli konuşma geçmişini içeren bir Remote Control oturumu başlatır.

    Bu komutla `--verbose`, `--sandbox` ve `--no-sandbox` bayrakları kullanılamaz.
  </Tab>

  <Tab title="VS Code">
    [Claude Code VS Code uzantısında](/docs/en/vs-code), istem kutusunda `/remote-control` veya `/rc` yazın ya da komut menüsünü `/` ile açın ve seçin.

    ```text theme={null}
    /remote-control
    ```

    İstem kutusunun üstünde bağlantı durumunu gösteren bir başlık görüntülenir. Bağlandıktan sonra, oturuma doğrudan gitmek için başlıkta **claude.ai/code** butonuna tıklayın veya [claude.ai/code](https://claude.ai/code) oturum listesinde bulun. Claude Code ayrıca oturum URL'sini konuşmada yayınlar.

    Bağlantıyı kesmek için başlıktaki kapat simgesini tıklayın veya `/remote-control` komutunu tekrar çalıştırın.

    CLI'nın aksine, VS Code komutu bir ad argümanını kabul etmez veya QR kodu görüntülemez. Oturum başlığı konuşma geçmişinden veya ilk isteminden türetilir.
  </Tab>
</Tabs>

### Bağlantı Durumunu Kontrol Edin

Interaktif bir terminal oturumunda, `/rc active` göstergesi bağlantı aktifken giriş kutusunun altındaki altbilgide bulunur ve terminal çok dar ise gizlenir. Gösterge metni oturuma claude.ai'daki bağlantıdır. Aşağı ok tuşu ile seçin ve Enter tuşuna basın veya başka bir cihazdan [bağlanmak için](#connect-from-another-device) `/remote-control` komutu tekrar çalıştırın, oturum URL'si ve QR kodu ile bir durum paneli açmak için. Durum paneli ayrıca bağlantıyı kesme seçeneği sunar. Bunu seçerek Remote Control'ü kapatın; yerel oturumunuz terminalinizde çalışmaya devam eder.

Bağlantı başarısız olursa, Claude Code başarısızlık nedenini gösteren bir bildirim gösterir ve göstergeyi başarısızlık durumuna değiştirir. Nedeni tekrar okumak için göstergeyi aşağı ok tuşu ile seçin ve Enter tuşuna basın. Yeniden bağlanmak için `/remote-control` komutunu çalıştırın; aksi takdirde [neden oturumun başka bir cihazda son bulduğunu veya sunucunun onu bulamadığını söylemek](#session-ended-elsewhere) durumunda olmadığı sürece.

<span id="session-ended-elsewhere" />Yeniden bağlanmadan önce nedeni okuyun. Oturum başka bir cihazdan veya Claude Code oturumundan alındığında ya da başka bir uygulama veya Claude Code oturumundan sonlandırıldığında, sunucu onu bulamadığında, neden bunu hangi durumda söyler ve Claude Code normal önerisini çıkarır `/remote-control` çalıştırmak:

* **Başka bir cihaz veya Claude Code oturumu oturumu aldı**: `/remote-control` yalnızca o cihazdan geri almak istiyorsanız çalıştırın.
* **Oturumu başka bir cihazdan veya uygulamadan sonlandırdınız veya arşivledirdiniz**: `/remote-control` yalnızca istiyorsanız çalıştırın; Claude Code arşivlenmiş bir oturumu yeniden açar.
* **Sunucu oturumu bulamaz**: başka bir cihazdan veya uygulamadan silinmiş olabilir.

### Oturum URL'si Anımsatıcıları

Remote Control bağlı durumdayken, Claude Code sizin telefonunuza veya tarayıcıya geçmek en iyi yardım ettiğinde oturum URL'sini anımsatır, böylece terminalde bağlantıyı beklemek yerine bağlantıdan takip edebilirsiniz. Aşağıdaki adımlardan birinde gösterilen bir anımsatma görüntülenir:

* **Uzun tur**: bir tur sunucu tarafından ayarlanmış bir eşikten daha uzun süre çalıştığında, Claude Code bir **Hala çalışıyor** bildirimi gösterir ve **Telefonunuzdan kontrol edin** bağlantısı ileti kutusunda görünür. Claude Code tur sonunda kaldırır.
* **Tekrarlanan izin istekleri**: bir oturumda birkaç [izin istemi](/docs/en/permissions)'ne yanıt verdikten sonra, bir **Telefonunuzdan araç çağrılarını onaylayın** bildirimi oturum URL'sini gösterir. Claude Code sonraki turunuz başladığında kaldırır.

Anımsatmalar, [otomatik olarak bağlanan](#enable-remote-control-for-all-sessions) Remote Control da dahil olmak üzere bağlı herhangi bir oturumda görüntülenebilir. Bu koşullar oluştuğu her zaman görüntülenmez ve her biri toplam oturumlar genelinde yalnızca birkaç kez görüntülenir. Yapılandıramaz veya kapatamaz; her biri kendi başına temizlenir.

### Başka Bir Cihazdan Bağlanın

Remote Control oturumu etkinken, başka bir cihazdan bağlanmanın birkaç yolu vardır:

* **Oturum URL'sini açın** [claude.ai/code](https://claude.ai/code)'daki oturuma doğrudan gitmek için herhangi bir tarayıcıda.
* **QR kodu tarayın** oturum URL'sinin yanında gösterilen Claude uygulamasında doğrudan açmak için. `claude remote-control` ile, QR kodu görüntüleme geçişi yapmak için spacebar tuşuna basın.
* **[claude.ai/code](https://claude.ai/code) veya Claude uygulamasını açın** ve oturum listesinde oturumu ada göre bulun. Claude mobil uygulamasında, oturum listesine ulaşmak için navigasyonda **Kod** (Code) seçeneğini dokunun. Remote Control oturumları, çevrimiçi olduğunda yeşil durum noktası olan bir bilgisayar simgesi gösterir.

Bağlanırken, cihaz oturumun zaten çalışan herhangi bir alt ajanı ve iş akışını gösterir.

Uzak oturum başlığı şu sırada seçilir:

1. `--name`, `--remote-control` veya `/remote-control` ilettiğiniz ad
2. `/rename` ile ayarladığınız başlık
3. Mevcut konuşma geçmişinde son anlamlı ileti
4. `myhost-graceful-unicorn` gibi otomatik oluşturulan ad; burada `myhost` makinenizin ana bilgisayar adı veya `--remote-control-session-name-prefix` ile ayarladığınız önektir

Açık bir ad ayarlamadıysanız, Claude Code başlığı bir ileti gönderdikten sonra istemcinizi yansıtmak için günceller. Claude Code otomatik oluşturulan başlıkları konuşmanızın diline eşleştirmek veya ayarlanmış bir [`language`](/docs/en/settings#available-settings) varsa ayarına; dil eşleştirmesi Claude Code v2.1.176 veya sonraki sürümleri gerektirir.

Bir oturumu claude.ai veya Claude uygulamasından yeniden adlandırırken, Claude Code yerel başlığı `claude --resume`'daki gösterildiği şekilde de günceller. Claude Code aynı yeniden adlandırmayı istem çubuğunda gösterilen oturum adına uygular ve [`claude agents`](/docs/en/agent-view) listesinde oturum [arka planda çalışırken](#resume-sessions-after-stopping-the-server). v2.1.221'den önce, claude.ai oturum listesinden veya Claude uygulamasından yeniden adlandırma yalnızca başlığı güncelledi ve CLI önceki oturum adını tuttu; `/rename` (CLI'de çalışan) herhangi bir sürümde adı ayarlar.

Henüz Claude uygulamaz yoksa, `/mobile` komutunu Claude Code içinde kullanarak [iOS](https://apps.apple.com/us/app/claude-by-anthropic/id6473753684) veya [Android](https://play.google.com/store/apps/details?id=com.anthropic.claude) için bir indirme QR kodu görüntüleyin.

### Bağlı Cihazların Gördüğü

Bağlı bir cihaz, terminalinizde yapılan konuşmayı gerçekleştiği sürece gösterir. Bu durumlar olağan iletilerden ötedir:

* **Yoğunlaştırma ve `/clear`**: Claude Code [konuşmayı yoğunlaştırırken](/docs/en/context-window#what-survives-compaction), bağlı cihazlar ilerlemeyi gösterir ve sonra konuşmanın nereden yoğunlaştırıldığını gösterir. `/clear` çalıştırdığınızda, konuşma bağlı cihazlarda de sıfırlanır.
* **`/resume` ile konuşmaları değiştirme**: bağlı cihaz geçilen konuşmanın başlığını veya önceki geçmişini almaz, ancak her iki yönde yeni iletiler terminalinizde hangi konuşma açık olursa olsun gider ve gelir. Cihazdan orijinal konuşmada çalışmak için, terminalinizde `/resume` çalıştırın ve geri dönün.
* **Diğer oturumlarınızdan iletiler**: [çapraz oturum iletişimi](/docs/en/cross-session-messaging) ile, aynı bağlantı diğer makinelerdeki oturumlarınız ve [Claude Code web'deki](/docs/en/claude-code-on-the-web) oturumlarınız arasında iletişim taşır, Anthropic sunucuları aracılığıyla Remote Control trafiğinin geri kalanı gibi. [Diğer Makinelerdeki Oturumları İletişim](/docs/en/cross-session-messaging#message-sessions-on-other-machines) teslim kurallarını ve [Gelen İletişimi Kontrol Edin](/docs/en/cross-session-messaging#control-inbound-messages) gelen denetimleri kapsar. Claude Code v2.1.224 veya sonraki sürümleri gerektirir.
* **Bağlantı Başarısızlığından Sonra Yeniden Bağlanma**: `/remote-control` komutu çalıştırın. Yoğunlaştırma konuşmayı veya `/resume` ile konuşmaları aradayken geçerli `claude remote-control` değiştirildi, Claude Code kullanmakta olduğu sunucu oturumunu bağlantıyı kesme yerine arşivler. Hala [arşivlenmiş oturumları filtreleyerek](/docs/en/claude-code-on-the-web#archive-sessions) bulabilirsiniz. Konuşmaları değiştirmek bir cihaz hala bağlı durumdayken oturumu arşivlemez.

### Tüm Oturumlar İçin Remote Control'ü Etkinleştirin

Remote Control, `/remote-control` komutunu çalıştırmadığı sürece, `claude --remote-control` veya `/remote-control`, otomatik bağlan kapalı olmadığı sürece etkinleştirilmez. Her interaktif oturum için otomatik bağlanmayı açmak için, Claude Code içinde `/config` komutunu çalıştırın ve **Tüm Oturumlar İçin Remote Control Etkinleştir** seçimini yapın. Geçiş üç değeri alır:

* **`true`**: interaktif oturum başladığında otomatik olarak bağlan.
* **`false`**: otomatik bağlanmayı kapatın, ancak [yönetilen ayarlardan](/docs/en/settings#settings-files) bir `true` üstün gelir, çünkü Claude Code seçimi kullanıcı ayarlarınıza kaydeder. Proje veya yerel ayarlarında bir `false` (`claude/settings.json`, `.claude/settings.local.json`) yönetilen bir `true` üzerinde bile otomatik bağlanmayı kapatır.
* **`default`**: seçiminizi temizleyin ve kuruluşunuzun yönetici varsayılanını takip edin, aksi takdirde Claude Code'un geçerli varsayılanını.

Aynı geçiş CLI dışında görüntülenir:

* **Masaüstü uygulaması**: **Ayarlar > Claude Code > Varsayılan Olarak Remote Control Etkinleştir**.
* **VS Code uzantısı**: [komut menüsünün](/docs/en/vs-code#use-the-prompt-box) Ayarlar bölümünde **Tüm Oturumlar İçin Remote Control Etkinleştir**. Claude Code v2.1.203 veya sonraki sürümleri gerektirir.

Bunun yerine ayarlar dosyasından otomatik bağlanmayı açmak için, kullanıcı `~/.claude/settings.json` veya [yönetilen ayarlarda](/docs/en/settings#settings-files) [`remoteControlAtStartup`](/docs/en/settings#available-settings) seçimini `true` olarak ayarlayın. Proje veya yerel ayarlarda (`.claude/settings.json`, `.claude/settings.local.json`), Claude Code bir `false` onurlandırır ve o depo için Remote Control'ü kapatır, ancak bir `true` yoksayar, bu nedenle kayıtlı dosya herkes için Remote Control'ü açamaz.

Otomatik bağlanma kendi claude.ai hesabınızla oturum açar, bu nedenle başlattığı oturum yalnızca kendi hesabınızın Claude uygulamalarında görünür ve kimseye başka erişim vermez.

Bu ayar açıkken, her interaktif Claude Code işlemi bir uzak oturum kaydeder. Birden çok örnek çalıştırırsanız, her biri kendi uzak oturumunu alır. Tek bir işlemden birden çok eş zamanlı oturum çalıştırmak için, bunun yerine [sunucu modunu](#start-a-remote-control-session) kullanın.

### Sunucuyu Durdurup Oturumları Yeniden Başlatın

`claude remote-control` ile Ctrl+C durduğunuzda, hizmet ettiği oturumlar telefonunuzdan veya tarayıcıdan yanıt vermeyi durdurur. Aynı dizinde başka bir `claude remote-control` çalıştırmadığınız ve bunu `--no-create-session-in-dir` ile başlatmadığınız sürece, Claude Code onları arşivlemez. Geri getirmek için, aynı dizinde aşağıdaki komutlardan birini çalıştırın:

* **`claude remote-control`**: sunucunun hizmet ettiği her oturumu geri getirin.
* **`claude remote-control --continue`**: sunucunun başlattığı oturumu geri getirin ve oturum sona erdiğinde çıkın. Bu dizinde hiçbir kayıt yoksa, Claude Code bu deponun diğer git worktree'lerinden en yenisini kullanır.
* **`claude remote-control --session-id <id>`**: ilettiğiniz oturum kimliğinin oturumunu geri getirin ve oturum sona erdiğinde çıkın. Kimlik oturumun URL'si claude.ai/code'da `/code/` ile herhangi bir `?` arasındaki bölümdür.

Bu komutlar sunucu durduğundan yaklaşık dört saat sonra çalışır. Bundan sonra, `claude remote-control` yeni bir oturum başlatmak için çalıştırın. Aradayken bir oturumu arşivlediyseniz, `--continue` ve `--session-id` Claude Code v2.1.228 veya sonraki sürümlerde arşivlenmiş oturumu çıkarır.

`claude --remote-control` veya `/remote-control` ile başlattığınız bir oturumu geri getirmek için, `claude --continue` veya `claude --resume` ile konuşmayı yeniden başlatın; Claude Code yeniden bağlanıp bağlanmadığı ve hangi oturuma bağlanıp bağlanmadığı konuşmanın [yeniden bağlanma kaydına](#resume-outcomes) bağlıdır. Remote Control hala ilk terminalinde açıksa ikinci terminalinde konuşmayı yeniden başlatırsanız, Claude Code ikinci terminalinde bir bildirim yazdırır ve Remote Control'ü kapatır. Remote Control'ü oraya taşımak için ikinci terminalinde `/remote-control` komutunu çalıştırın.

Claude Desktop veya Remote Control açık olduğu bir IDE uzantısında konuşmayı yeniden başlatırsanız, Claude Code yeni bir tane eklemek yerine mevcut claude.ai oturumuna yeniden ekler.

## Bağlantı ve Güvenlik

Yerel Claude Code oturumunuz yalnızca giden HTTPS istekleri yapar ve makinenizde hiçbir gelen port açmaz. Remote Control başlattığınızda, Anthropic API'yi kaydeder ve çalışma için yoklar. Başka bir cihazdan bağlandığınızda, sunucu iletileri web veya mobil istemci ile yerel oturumunuz arasında bir akış bağlantısı üzerinden yönlendirir.

Tüm trafik Anthropic API üzerinden TLS aracılığıyla, herhangi bir Claude Code oturumu olarak aynı taşıma güvenliği ile seyahat eder. Bağlantı, her biri tek bir amaçla kapsamlı ve bağımsız olarak sona eren birden çok kısa ömürlü kimlik bilgisini kullanır.

Remote Control bağlı durumdayken, oturum transkripti (iletileriniz, Claude'un yanıtları ve araç etkinliği dahil olmak üzere) Anthropic sunucularında depolanır. Depolanan transkript konuşmayı cihazlarınız arasında senkronize tutar ve oturumun ağ düşüşünden sonra yeniden bağlanmasını sağlar. Yürütme ve dosya sistemi erişimi makinenizde kalır ve depolanan transkriptler [Veri Kullanımı](/docs/en/data-usage) politikası kapsamında tutulur.

Remote Control'ü tamamen kapatmak için [`disableRemoteControl`](/docs/en/settings#available-settings) ayarını kullanın. Zero Data Retention gibi uyum gereksinimleri olan kuruluşlar Remote Control'ü etkinleştiremez.

## Güvenilir Cihazlar

<Note>
  Güvenilir Cihazlar şu anda beta aşamasındadır. Özellikler ve işlevsellik, deneyim iyileştirilirken değişebilir.

  Güvenilir Cihazlar Team ve Enterprise planlarında mevcuttur. Varsayılan olarak kapalıdır, bir yönetici bunu etkinleştirene kadar.
</Note>

Güvenilir Cihazlar, üyelerin claude.ai, Claude mobil uygulamaları veya Claude Desktop'tan Remote Control oturumlarını görüntülemeden veya yönlendirmeden önce cihazlarını doğrulamalarını gerektiren kuruluş genelinde bir ayardır. Remote Control erişimini bir bilinen cihaza ve son kimlik doğrulaması ile bağlar, sadece oturum açmış bir hesapla değil.

Ayar açık olduğunda, bir Remote Control oturumu ile etkileşim kurmak aşağıdakilerin her ikisini gerektirir:

* **Kayıtlı bir cihaz**: her üyenin Remote Control için kullandığı tarayıcı, telefon veya masaüstü uygulaması kendi kimlik bilgisini kaydeder. Kayıt yalnızca tam oturum açmadan kısa bir süre sonra sunulur, bu nedenle bir cihaz sessizce arka planda değil, gerçek kimlik doğrulamanın bir parçası olarak güvenilir listeye katılır.
* **Son kimlik doğrulama**: üyenin oturum açması en fazla 18 saat eski olmalıdır. Her gün yeniden oturum açmak yerine, üyeler Face ID, Touch ID, Windows Hello veya bir geçit anahtarı ile varlık onaylar. Bu biyometrik adım hemen oturumu yeniler.

Biyometrik kontroller cihaz aracılığıyla işletim sistemi veya tarayıcı tarafından çalıştırılır, geçit anahtarı oturum açma ile aynı mekanizmayla. Anthropic hiçbir zaman parmak izini, yüz verilerini veya diğer biyometrik bilgileri almaz veya depolamaz. Yalnızca cihazın ortak anahtarı ve ad, platform ve kayıt saati gibi temel meta veri depolanır.

Ayar yalnızca Remote Control'ü etkiler. Normal Claude sohbeti, terminaldeki Claude Code ve API kullanımı etkilenmez.

### Kuruluşunuz İçin Güvenilir Cihazları Etkinleştirin

Yöneticiler ayarı Claude Code yönetici konsolundan etkinleştirir.

<Steps>
  <Step title="Claude Code Yönetici Ayarlarını Açın">
    [claude.ai/admin-settings/claude-code](https://claude.ai/admin-settings/claude-code) adresine gidin. **Güvenilir Cihazlar Gerekli** geçişi Remote Control ayarı altında görüntülenir.
  </Step>

  <Step title="Güvenilir Cihazlar Gerekliyi Açın">
    Ayar kuruluşun her üyesi ve açtıktan sonra başlayan Remote Control oturumlarına uygulanır. Geçiş açılmadan önce zaten çalışan oturumlar geriye dönük olarak korunmaz ve cihaz gereksinimi olmadan cihaz gereksinimi sona erene kadar devam eder.
  </Step>

  <Step title="Üyelere Ne Bekleyeceğini Söyleyin">
    Geçiş etkinleştirildikten sonra bir üye tarayıcı, telefon veya masaüstü uygulamasından ilk kez yeni bir Remote Control oturumunu görüntüler veya yönetir, cihazı kaydı istenir. Bunun konusunda önceden söylemek kafa karışıklığını önler.
  </Step>
</Steps>

### Üyelerin Gördüğü

Kayıt cihaz başına tek seferlik bir adımdır. Bundan sonra, tek görünen değişiklik ara sıra bir biyometrik istemidir.

* **Her cihazda ilk kullanım**: üye kaydolması istenir. Oturum açmaları son zamanlarda değilse, genellikle oturum açma akışınızı (SSO dahil) oturumdan sonra kaydı onaylar.
* **Gün içinde**: kayıtlı cihazı ve son oturum açması olan üyeler hiçbir istem görmez. Oturum açma 18 saati geçtiğinde, sonraki Remote Control etkileşimi tek bir Face ID, Touch ID, Windows Hello veya geçit anahtarı istemidir.
* **Kayıtlı Olmayan Cihazlar**: Remote Control oturumları cihaz kaydolana kadar görüntülenmez veya yönetilmez. Düzenli Claude sohbeti o cihazda etkilenmez.
* **Platformu Doğrulayıcısı Yok**: Face ID, Touch ID veya Windows Hello olmayan makinedeki üyeler donanım güvenlik anahtarını kullanabilir veya açacak yerine yeniden oturum açabilir.
* **Terminalinde**: Claude Code çalıştıran makine, geliştirici CLI'ye oturum açtığında otomatik olarak kendi kimlik bilgisini alır. Terminalde ayrı bir kayıt adımı yoktur.

### Kayıtlı Cihazları Yönetin

Üyeler kendi cihazlarını hesap ayarlarından gözden geçirebilir ve iptal edebilir.

[claude.ai/settings/account](https://claude.ai/settings/account#trusted-devices) adresini açın ve **Güvenilir Cihazlar** bölümünü bulun, her kayıtlı cihazı ad, platform ve kayıt tarihiyle görüntüleyebilirsiniz. Bir cihazı kaldırmak hemen kimlik bilgisini iptal eder ve cihaz daha sonra taze oturum açmadan yeniden kaydolabilir. Kimlik bilgileri ayrıca kullanılmıyorsa kendi başlarına sona erer, bu nedenle kullanılmayan bir cihaz güvenilir listeden otomatik olarak düşer.

Kayıp veya çalıntı bir cihaz için üye bunu bu sayfadan kaldırır. Üye oturum açamıyorsa, yönetici yönetici konsolunda **Her Yerde Oturum Kapat** seçeneğini kullanarak o üyeye ait her oturumu ve kayıtlı cihazı iptal edebilir, bundan sonra üye tuttuğu cihazları yeniden kaydeder.

## Remote Control vs Claude Code Web'de

Remote Control ve [Claude Code web'de](/docs/en/claude-code-on-the-web) ikisi de claude.ai/code arayüzünü kullanır. Temel fark oturumun nerede çalıştığıdır: Remote Control makinenizde yürütülür, bu nedenle yerel MCP sunucularınız, araçları ve proje yapılandırması mevcuttur. Claude Code web'de bulutu yürütülür.

Yerel çalışmanın ortasında olan ve başka bir cihazdan devam etmek istiyorsanız Remote Control'ü kullanın. Herhangi bir yerel kurulum yapmadan görev başlatmak, klonlanmayan bir depoda çalışmak veya birden çok görev paralel olarak çalıştırmak istiyorsanız Claude Code web'de kullanın.

## Mobil Anında İletişim Bildirimleri

Remote Control etkinken, Claude telefonunuza anında iletişim bildirimleri gönderebilir.

Claude bildirimin ne zaman gönderileceğini belirler. Genellikle uzun süreli görev tamamlandığında veya devam etmek için sizden bir karar gerektiğinde gönderir. Ayrıca bir istemde "testler bittiğinde beni bilgilendir" örneğin bildirim isteyebilirsiniz. Aşağıdaki iki açma/kapatma geçişi ötesinde olay başına yapılandırma yoktur.

Mobil anında iletişim bildirimlerini ayarlamak için:

<Steps>
  <Step title="Claude Mobil Uygulamasını Yükle">
    [iOS](https://apps.apple.com/us/app/claude-by-anthropic/id6473753684) veya [Android](https://play.google.com/store/apps/details?id=com.anthropic.claude) için Claude uygulamasını indir.
  </Step>

  <Step title="Claude Code Hesabınızla Oturum Açın">
    Terminal'de Claude Code kullandığınız aynı hesapla ve kuruluşla kullan.
  </Step>

  <Step title="Bildirimlere İzin Ver">
    İşletim sisteminizden bildirimleri izni istemini kabul et.
  </Step>

  <Step title="Claude Code'da Anında İletişimi Etkinleştir">
    Terminalinizde `/config` çalıştırın ve proaktif bildirimler için **Claude Karar Verdiğinde Gönder**, izin istekleri ve sorular için **Eylem Gerektiğinde Gönder** veya ikisini de etkinleştir.
  </Step>
</Steps>

Bildirimler gelmezse:

* `/config` **Kayıtlı Mobil Yok** gösteriyorsa, telefonunuzdaki Claude uygulamasını açın, böylece anında iletişim tokenini yenileyebilir. Uyarı, Remote Control bağlı olduğunda temizlenir.
* iOS'ta, Odaklanma modları ve bildirim özetleri gönderileri gizleyebilir veya geciktirebilir. Ayarlar → Bildirimler → Claude kontrol edin.
* Android'te, agresif pil optimizasyonu teslim etmeyi geciktirebilir. Claude uygulamasını sistem ayarlarında pil optimizasyonundan muaf tutun.

Claude Code, bağlı terminalinizi yazarken veya odaklandığında mobil anında iletişim bildirimlerini atlar. v2.1.181'den itibaren, makinenizde herhangi bir zamanda, başka bir pencerede bile olsa, dosyanız varlığında öznitelik olarak ayarlamak için [`CLAUDE_CLIENT_PRESENCE_FILE`](/docs/en/env-vars) ayarlayabilirsiniz: bildirimler dosya varken atlanır. Ekran kilidi açtığında dosyayı oluşturmak ve ekran kilitlendiğinde silmek için ekran kilidi dinleyici veya benzer araç yapılandırın.

## Sınırlamalar

* **Interaktif işlem başına bir uzak oturum**: sunucu modu dışında, her Claude Code örneği aynı anda bir uzak oturumu destekler. Tek bir işlemden birden çok eş zamanlı oturum çalıştırmak için [sunucu modunu](#start-a-remote-control-session) kullanın.
* **Yerel işlem çalışmaya devam etmelidir**: Remote Control yerel işlem olarak çalışır. Terminal kapatırsanız, VS Code'dan çıkarsanız veya aksi takdirde `claude` işlemini durdurunuz, oturum [geri getirene kadar](#resume-sessions-after-stopping-the-server) çevrimdışı görülür. SSH'den bağlantıyı kestikten sonra oturumun uzak makinede çalışmaya devam etmesini sağlamak için bunu `tmux` veya `screen` içinde başlatın.
* **Genişletilmiş ağ kesintisi**: makineniz uyanıksa ancak ağa erişemiyorsa, sonra ne yapacağını, moduna bağlıdır:
  * **Sunucu modu**: Claude Code yaklaşık 10 dakika sonra bırakır ve `claude remote-control` işlemi çıkar. Yeni bir oturum başlatmak için `claude remote-control` çalıştırın.
  * **İnteraktif oturum**: yerel olarak çalışmaya devam edin. Claude Code kesinti süresince yeniden dener ve ağ geri geldiğinde otomatik yeniden bağlanır.
* **Varlık sinyallerinin başarısız olması**: interaktif oturum `Remote Control sunucusuna yaklaşık 30 dakika boyunca erişemedi` bildiremesinde bağlantı kesilirse, `/remote-control` çalıştırın. Claude Code yalnızca oturumun varlık sinyalinin başarısız olması durumunda bu iletiyi gösterir, geri kalanı bağlı kalırken; yaklaşık 30 dakika sonra oturumu yeniden kaydeder.
* **Yönlendirilen diyaloglar sona erer**: Claude Code izin istemlerini ve `AskUserQuestion` sorularını açık tutar. Claude Code başka tür diyaloğu uzak oturuma ilettiğinde, örneğin güvenlik reddinden sonra gösterilen model seçim istemi, varsayılan olarak beş dakika bekler, sonra diyaloğu kapatır ve diyaloğun hiçbir eylem varsayılanı ile devam eder. Tutmayı veya devre dışı bırakmak için [`dialogExpiry`](/docs/en/settings#available-settings) ayarını yapın. Claude Code v2.1.224 veya sonraki sürümleri gerektirir. Tutulan çapraz oturum iletişimi için onay diyaloğu aynı son tarihi kullanır. [Tutulan ileti son tarihi kuralları](/docs/en/cross-session-messaging#control-inbound-messages) Claude Code diyaloğu son tarihten sonra açık tuttuğu durumları kapsar.
* **Bazı komutlar yalnızca yereldir**: `/plugin` veya `/resume` gibi yalnızca terminal arayüzünde çalışan komutlar herhangi bir argüman geçirseniz veya geçmezseniz yalnızca yerel CLI'dan çalışır. Aşağıdakiler mobil ve web'den çalışır:
  * Metni çıkaran komutlar: `/compact`, `/clear`, `/context`, `/usage`, `/exit`, `/usage-credits` (tarayıcıyı açmak yerine faturalandırma URL'sini yazdırır), `/recap`, `/reload-plugins`
  * `/model`, `/effort`, `/fast`, `/color` ve `/rename`: argümanı bir argüman olarak geçir, örn. `/model sonnet` veya `/effort high`. Mobil ve web'den, `/model` ve `/effort` argümanın yerini alır.
  * v2.1.166'dan `/mcp`: mobil uygulamadan, sunucu durumunun metin özeti döndürülür. Web'de, `/mcp` kendi başına [claude.ai bağlayıcıların](/docs/en/mcp#use-mcp-servers-from-claude-ai) dizinini açar, özeti döndürmek yerine. `reconnect`, `enable` ve `disable` [alt komutları](/docs/en/commands#all-commands) her ikisinden de çalışır. Yerel CLI'nın aksine, `/mcp reconnect` sunucu adı olmadan başarısız olmuş veya kimlik doğrulama gerekli olan her sunucuyu yeniden bağlar.
  * v2.1.181'den `/config`: mobil uygulamadan, ayar yapmak için `key=value` geçir veya ayarlayabileceğiniz anahtarları listelemek için argüman olmadan çalıştır. Web'de, `/config` komutu yerini ayarlarınız başlıklı Claude Code bölümüne açar ve komuttan sonraki metni yoksayar.
  * Team ve Enterprise'da, mobil veya web'den `/usage-credits`, yöneticiye [kullanım kredileri isteği](/docs/en/costs#add-usage-credits-to-your-subscription) göndermez. Gönderme, yalnızca interaktif CLI'de görünen onay gerektirir, bu nedenle komut bunun yerine orada çalıştırmanızı söyler. v2.1.211'den önce, metni şekli onay olmadan istek gönderdi.
  * v2.1.221'den `/autocompact`: argüman olarak pencere boyutunu geçir, örn. `/autocompact 500k`. Argüman olmadan, geçerli pencere boyutunu metin olarak yazdırır, terminal oturumunun gösterdiği diyaloğu açmak yerine.

## Sorun Giderme

### "Remote Control bir claude.ai aboneliği gerektirir"

claude.ai hesabıyla doğrulanmadınız. `claude auth login` çalıştırın ve claude.ai seçeneğini seçin. `ANTHROPIC_API_KEY` ortamında ayarlıysa, önce ayarlamayı kaldırın.

v2.1.206'dan önce, imzalı olmayan durumdayken `/remote-control` çalıştırmak `Bilinmeyen komut: /remote-control` yerine bu iletiyi rapor etmiştir.

### "Remote Control tam kapsam oturum açma tokenı gerektirir"

`claude setup-token` veya `CLAUDE_CODE_OAUTH_TOKEN` ortam değişkeninden uzun ömürlü bir token ile doğrulanıyor. Bu tokenler yalnızca model istekleri yapabilir, bu nedenle Remote Control oturumları kuramaz. Tam kapsam oturum açma tokenı ile doğrulanmak için `claude auth login` komutunu çalıştırın.

### "Kuruluşunuzu Remote Control uygunluğu için belirlenemiyor"

Önbelleğe alınmış hesap bilgileriniz eski veya eksiktir. Yenilemek için `claude auth login` komutunu çalıştırın.

### "Remote Control henüz hesabınız için etkinleştirilmedi"

Remote Control yayını hesabınıza henüz ulaşmamıştır veya önbelleğe alınmış başlıklarınız güncel değildir. Son zamanlarda plan değiştirdiyseniz, bunları yenilemek için `claude auth logout` ve sonra `claude auth login` komutlarını çalıştırın. Başarısız olan bireysel uygunluk kontrolünü görmek için `claude doctor` komutunu çalıştırın. Ortam değişkeni çatışmaları, ulaşılamayan kontroller ve kuruluş politikası her biri kendi iletisini üretir, bu nedenle bu hata yayın kapısı anlamına gelir. v2.1.154'ten önce, `DISABLE_TELEMETRY` veya `DO_NOT_TRACK` gibi özellik bayrağı değerlendirmesini devre dışı bırakan bir değişken de bu iletiyi üretmiştir; "Remote Control özellik bayrağı değerlendirmesi gerektirir" girişi aşağıda bu yapılandırmayı kapsar.

### "Remote Control uygunluğu doğrulana mamazdı"

Claude Code özellik bayrağı hizmetine ulaşamadı, genellikle çevrimdışı olduğunuz veya proxy istei bloke ettiği için. Ağ erişimi alıp yeniden deneyin veya ayrıntılar için `claude doctor` komutunu çalıştırın. İlgili "Kuruluşunuzun Remote Control politikası doğrulanamadı" iletisinin aynı sebebi ve aynı düzeltmesi vardır. Her iki ileti de v2.1.178'de eklendi.

### "Remote Control özellik bayrağı değerlendirmesi gerektirir"

Bunlardan biri ayarlanmıştır: [`DISABLE_TELEMETRY`, `DO_NOT_TRACK`, `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` veya `DISABLE_GROWTHBOOK`](/docs/en/env-vars). Her biri, Remote Control kullanılabilirliğinin bağlı olduğu özellik bayrağı değerlendirmesini devre dışı bırakır ve tam ileti Claude Code'un bulduğu değişkeni adlandırır. Değişkeni kabuğu ortamında veya [`settings.json`](/docs/en/settings#available-settings) dosyasının `env` bloğunda ayarlı olduğu yerde ayarlamayı kaldırın. v2.1.154'ten önceki sürümlerde, aynı yapılandırma "Remote Control hesabınız için henüz etkinleştirilmedi" yerine üretilir.

### "Remote Control yalnızca Claude api.anthropic.com aracılığıyla kullanılabilir"

Oturum doğrudan Anthropic API ile konuşmaz, bu nedenle eşleştirilecek claude.ai arka ucu yoktur. Bu Amazon Bedrock, Google Cloud'ın Agent Platform ve Microsoft Foundry'de gerçekleşir. Ayrıca [`ANTHROPIC_BASE_URL`](/docs/en/env-vars), `api.anthropic.com` dışında bir ana bilgisayara işaret ettiğinde de gerçekleşir (örn. [LLM ağ geçidi](/docs/en/llm-gateway) veya proxy gibi), claude.ai ile oturum açsanız bile. v2.1.196'dan önce Claude Code özel `ANTHROPIC_BASE_URL` için bu iletiyi göstermedi. Tam neden listesi için [hata referansına](/docs/en/errors#remote-control-requires-the-anthropic-api) bakın.

İleti oturumu Anthropic API'den uzaklaştırdığını adlandırır, `CLAUDE_CODE_USE_BEDROCK` veya özel `ANTHROPIC_BASE_URL` gibi. Uygun bir claude.ai oturum açmanız varsa, adlandırılmış değişkeni ayarlamayı kaldırın, [ayarlardan](/docs/en/settings) ayarlı ise `env` anahtarından kaldırın ve oturumu yeniden başlatın. v2.1.219'dan önce, ileti yalnızca bu bölüm başlığındaki cümledir, bu nedenle eski sürümlerde `CLAUDE_CODE_USE_BEDROCK` ve `CLAUDE_CODE_USE_VERTEX` gibi sağlayıcı değişkenlerini kendi ortamında ve `ANTHROPIC_BASE_URL`'yi kontrol edin.

### "Remote Control kuruluşunuzun politikası tarafından devre dışı bırakılmıştır"

Bir politika Remote Control'ü engeller. İletinin kendi metni hangisini söyler:

* **Hata `disableRemoteControl` söylemiyorsa**: BT yöneticininiz bu cihazda [yönetilen ayarlar](/docs/en/settings#settings-files) aracılığıyla Remote Control'ü devre dışı bırakmıştır, kuruluş genelinde geçişinden ve oturum açtığınız şekliyle bağımsız.
* **Aksi takdirde, bir Sahip kuruluşunuz için bunu etkinleştirmemiştir**: bu form görüntülendiğinde, uygun bir claude.ai hesabıyla oturum açtığınızda ancak Remote Control kapalı olur, Team ve Enterprise planlarında varsayılan. Bir Sahip [claude.ai/admin-settings/claude-code](https://claude.ai/admin-settings/claude-code) adresinde **Remote Control** geçişini açarak bunu etkinleştirebilir. Bu geçiş sunucu taraflı kuruluş ayarıdır.

### "Remote Control kuruluşunuzun uyum politikası nedeniyle kullanılamaz"

Kuruluşunuz Remote Control ile uyumlu olmayan veri saklama veya uyum yapılandırmasına sahiptir; iletinin sonundaki parantez içindeki adlandırması. Bu durumdayken yönetici panelinin Remote Control geçişi gri renkte olur, bu nedenle bir Sahip bunu değiştiremez. Seçenekleri tartışmak için Anthropic desteği ile iletişime geçin.

### "Uzak kimlik bilgileri getirme başarısız oldu"

Claude Code Anthropic API'den bağlantı kurulacak kısa ömürlü kimlik bilgisini alamadı. `-verbose` bayrağıyla yeniden çalıştırın:

```bash theme={null}
claude remote-control --verbose
```

Yaygın nedenler:

* Oturum açılmamış: claude.ai hesabınızla doğrulanmak için `claude` ve `/login` komutlarını çalıştırın. API anahtarı kimlik doğrulaması Remote Control'ü desteklemez.
* Ağ veya proxy sorunu: bir güvenlik duvarı veya proxy giden HTTPS istemi bloke edebilir. Remote Control Anthropic API'ye 443 portunda erişim gerektirir.
* Oturum oluşturması başarısız oldu: ayrıca `Oturum oluşturması başarısız — hata ayıklama günlüğünü bakın` gösteriyorsa, başarısızlık daha önce kurulumda meydana geldi. Aboneliğinizin aktif olduğunu kontrol edin.

Eski oturum açma tokenı bu hataya neden olmaz. Anthropic API kaydedilen tokenı reddediğinde, örneğin başka bir Claude Code işlemi onu zaten yeniledikten sonra, Claude Code token yeniler ve otomatik yeniden dener. v2.1.224'ten önce, eski token Remote Control başlangıç başarısızlığı ile başarısız ve [otomatik olarak bağlanan](#enable-remote-control-for-all-sessions) oturumlar arada ağır başarısız olabilir.

### "Uzak kontrol oturumunuza yeniden bağlanamadı"

`claude --resume` veya `claude --continue` ile konuşmayı yeniden başlattığınızda, Claude Code o konuşmaya kaydedilen Remote Control oturumuna yeniden bağlanır. Bu ileti yeniden bağlanma başarısız bir ağ kesintisi gibi geçici bir neden için başarısız anlamına gelir, bu nedenle Claude Code uzak oturumun hala varsa doğrulayamaz.

Bağlantıyı yeniden denemek veya yeni bir Remote Control oturumu oluşturmak için `claude --remote-control` çalıştırın `/remote-control` komutunu çalıştırın; yerel oturumunuz arada Remote Control olmadan çalışmaya devam eder.

<span id="resume-outcomes" />Yeniden başladığınızda bu ileti yerine bu sonuçlardan birini de alabilirsiniz:

* **Sunucu kaydedilen oturum gitti rapor eder veya yeniden bağlanma kaydı farklı bir hesabı adlandırır**: Claude Code konuşmanın yeniden bağlanma kaydının söylediğine göre:
  * **Kayıt oturum açtığınız hesabı adlandırır**: Claude Code oturumun önceki iletileri hariç olmak üzere otomatik oluşturulan adla bir yenisini başlatır. Bu, örneğin, oturumu claude.ai veya Claude uygulamasından sildikten sonra olur.
  * **Kayıt farklı bir hesabı adlandırır**: Claude Code oturumun önceki iletileri olmadan yeni bir oturum başlatır ve oturumun hala var olup olmadığı göstermez.
  * **Kayıt hangi hesabın oturuma sahip olduğunu söylemez veya Claude Code kaydedilen oturum açmanız okuyamaz**: Claude Code [`Önceki oturum kullanılamaz — yeni bir oturum başlatmak için /remote-control çalıştırın`](#previous-session-is-unavailable) yerine bu iletiyi gösterir, hiçbir şey başlatmaz ve kaydı konuşmadan kaldırır.
* **Remote Control'ü kapatmadan başlamadan önce kapattınız**: CLI'nın [durum paneli](#check-connection-status), VS Code uzantısı veya [Agent SDK](/docs/en/agent-sdk/overview) üzerine inşa edilen bir ana bilgisayar olmayan bir üzerine bir oturum sahip olmadığı sürece, Claude Code kaydı çıkardı, bu nedenle yeniden bağlanmaz. Sahip ana bilgisayar kapatıldığında, Claude Code kaydı tuttu ve yeniden bağlanır.
* **Bu makinedeki başka bir Claude Code zaten oturuma sahiptir**: Remote Control etkinleştirilmediğinde bir [`Uzak kontrol burada başlatılmadı`](#resume-sessions-after-stopping-the-server) bildirim ile başlayan bir bildirim alırsınız; Claude Code yeniden başlama oturumundaki Remote Control'ü kapatır. Oraya taşımak için `/remote-control` çalıştırın.

<span id="reconnect-history" />v2.1.232'den önce, Claude Code kaydedilen oturum gitti rapor edildiğinde farklı yanıt verdi. v2.1.227 aracılığıyla v2.1.231'den, Claude Code kayıt hesabınızla eşleşse bile bir değişiklik başlatmayı reddetti. v2.1.226'dan önceki, kayıt hesabınızla eşleşip eşleşmediğine bakılmaksızın bir değişiklik başlattı ve v2.1.224 aracılığıyla v2.1.226'da başka hesabın altında değil o makinede oturum açmış hesabın altında oluşturduk, konuşmanın önceki iletileri yüklemedi. v2.1.200'den önce, Claude Code herhangi bir yeniden bağlanma başarısızlığından sonra yeni bir oturum oluşturdu.

<h3 id="previous-session-is-unavailable">
  "Önceki oturum kullanılamaz — yeni bir oturum başlatmak için /remote-control çalıştırın"
</h3>

Claude Code önceki Remote Control oturumuna geri getiremedi ve çalıştırılan yenisini bir kendi başına başlatmak yerine durdu. `claude --resume` veya `claude --continue` ile konuşmayı yeniden başlattıktan sonra veya Claude Code [bir kopya sonra otomatik yeniden bağlanmasından](#remote-control-couldnt-refresh-your-login) sonra bu iletiyi görebilirsiniz.

Yeni bir Remote Control oturumu başlatmak için `/remote-control` komutunu çalıştırın; yerel oturumunuz arada Remote Control olmadan çalışmaya devam eder. İlgili ileti `Remote Control oturum açmış hesabı doğrulayamadı — yeniden bağlanmak için /remote-control çalıştırın` aynı düzeltmeye sahiptir; Claude Code oturum açmış hesap doğrulanması ile yeniden bağlanması arasında değiştiğinde veya okunamadığında gösterir. Claude Code önce yeniden başlatmadan `Önceki oturum kullanılamaz` sonra `/remote-control` çalıştırırsanız, Claude Code konuşmanın önceki iletilerini yeni oturum dışında bırakır.

Yeniden başlamada, Claude Code [yeni bir oturum yerine başlatar](#resume-outcomes) yalnızca oturumun yeniden bağlanma kaydısı o hesabının adını konuşmanızın adı tutarsa, çünkü sunucu kayıt etmemiş bir oturum ve başka bir hesap tarafından sahip olunan bir oturumu aynı şekilde rapor eder. Claude Code v2.1.227'den önce bu hesabı kaydetmedi ve Claude Code kaydedilen oturum açmanızı okuyamaz. Claude Code v2.1.232'den önce `Uzak kontrol oturumu geçerli oturum açma altında yeniden başlatılamadı — taze başlamak için /remote-control çalıştırın` [farklı bir durumlar seti](#reconnect-history) gösterilir.

### "Remote Control beklenmedik sunucu yanıtı aldı"

Remote Control sunucusu istemi kabul etti ancak uzak oturum oluşturma veya kimlik bilgisini getirme sırasında bu Claude Code sürümü okuyamadığı bir formda yanıt verdi. Aynı sürümde yeniden deneme başarısız olur. `claude update` çalıştırın, sonra yeniden bağlanmak için `/remote-control` komutunu çalıştırın. Bu ileti v2.1.225'te eklendi.

### "Kuruluşunuz Remote Control için Güvenilir Cihazları gerektiriyor ancak bu cihaz kayıtlı değildir"

Kuruluşunuz [Güvenilir Cihazları](#trusted-devices) etkinleştirdi ve bu makine henüz kayıt olmadı. Claude Code içinde `/login` komutunu çalıştırın. Kayıt oturum açmaya bir parça olur ve ayrı bir kayıt komutu yoktur.

### "Güvenilir cihaz kontrolü için oturum sona erdi"

Oturum açmanız 18 saatten daha eski. Claude Code içinde `/login` komutunu çalıştırın veya claude.ai veya mobil uygulama Face ID, Touch ID, Windows Hello veya geçit anahtarıyla istediğinde onaylayın. Bkz. [Güvenilir Cihazlar](#trusted-devices).

## Doğru Yaklaşımı Seçin

Claude Code, terminalde değilken çalışmanın birkaç yolu sunar. Çalışmayı tetikleyen, Claude'un nerede çalıştığı ve kurulumu ne kadar gerekli olduğuna göre farklılık gösterirler.

|                                                          | Tetikleyici                                                                                        | Claude çalışır                                                                               | Kurulum                                                                                                                                | En İyi                                                      |
| :------------------------------------------------------- | :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------ |
| [Gönder](/docs/en/desktop#sessions-from-dispatch)           | Claude mobil uygulamasından görev iletişim                                                      | Makineniz (Desktop)                                                                       | [Mobil Uygulamayı Desktop ile Eşleştir](https://support.claude.com/en/articles/13947068)                                                  | Uzakta iken çalışmayı devretme, minimal kurulum              |
| [Remote Control](/docs/en/remote-control)                     | Çalışan oturumu [claude.ai/code](https://claude.ai/code) veya Claude mobil uygulamasından yönlendir | Makineniz (CLI veya VS Code)                                                                | `claude remote-control` çalıştırın                                                                                                          | Başka bir cihazdan çalışan iş yönlendir                |
| [Kanallar](/docs/en/channels)                                 | Telegram veya Discord gibi sohbet uygulamasından veya kendi sunucunuzdan etkinliği gönder                       | Makineniz (CLI)                                                                           | [Kanal eklentisi yükle](/docs/en/channels#quickstart) veya [kendi oluştur](/docs/en/channels-reference)                                      | CI başarısızlıkları veya sohbet iletileri gibi dış olaylara tepki verme |
| [Slack](/docs/en/slack)                                       | Takım kanalında `@Claude` bahset                                                            | Anthropic Bulut                                                                              | [Slack uygulamasını yükle](/docs/en/slack#setting-up-claude-code-in-slack) ve [Claude Code web'de etkinleştir](/docs/en/claude-code-on-the-web) | Takım sohbetinden PR'ler ve incelemeler                                |
| [Kendi barındırılan ortamlar](/docs/en/self-hosted-environments) | Bir [bulut oturumu](/docs/en/claude-code-on-the-web) başlatın ve kuruluşunuzun ortamını seçin   | Kuruluşunuzun altyapısı                                                                       | [Koşucular dağıtın](/docs/en/self-hosted-environments-quickstart), Team ve Enterprise planlarında                                              | Ağınızda çalışması gereken bulut oturumları              |
| [Zamanlanan görevler](/docs/en/scheduled-tasks)                   | Zamanlama ayarla                                                                                 | [CLI](/docs/en/scheduled-tasks), [Desktop](/docs/en/desktop-scheduled-tasks) veya [bulut](/docs/en/routines) | Sıklık seçin                                                                                                                     | Günlük incelemeler gibi tekrarlanan otomasyon                       |

## İlgili Kaynaklar

* [Claude Code Web'de](/docs/en/claude-code-on-the-web): makinenizin yerine bulutta oturumları çalıştırın, [bulut ortamları](/docs/en/cloud-environments) aracılığıyla yapılandırılmış
* [Çapraz Oturum İletişimi](/docs/en/cross-session-messaging): Claude diğer makinelerdeki veya [Claude Code Web'deki](/docs/en/claude-code-on-the-web) oturumlarınıza ileti gönderme
* [Kanallar](/docs/en/channels): Telegram, Discord veya iMessage'i bir oturuma iletme, böylece Claude uzakta iken iletilere tepki verir
* [Gönder](/docs/en/desktop#sessions-from-dispatch): telefonunuzdan bir görev iletişim ve Desktop oturumu işlemek için oluşturabilir
* [Kimlik Doğrulama](/docs/en/authentication): `/login` kurulumu ve claude.ai hesapları yönetimi
* [CLI Referansı](/docs/en/cli-reference): `claude remote-control` dahil tüm bayrakları ve komutları
* [Güvenlik](/docs/en/security): Remote Control oturumlarının Claude Code güvenlik modeline nasıl uyduğu
* [Veri Kullanımı](/docs/en/data-usage): yerel ve uzak oturumlar sırasında Anthropic API aracılığıyla ne kadar veri akar
