### 날짜 :  2022-08-18 09:18

### 인덱스 :

### 태그 : #ec-cube, #costomize, #Entity, #Repository

----

### 메모 :
새롭게 데이터를 추가할 엔티티와 리포지토리를 만들자

\\app\\Customize\\Entity\\StoreEntry.php
```php
<?php

namespace Customize\Entity;

use Doctrine\ORM\Mapping as ORM;

if (!class_exists('\Customize\Entity\StoreEntry')) {
    /**
     * StoreEntry
     *
     * @ORM\Table(name="c_dtb_store_entry")
     * @ORM\InheritanceType("SINGLE_TABLE")
     * @ORM\DiscriminatorColumn(name="discriminator_type", type="string", length=255)
     * @ORM\HasLifecycleCallbacks()
     * @ORM\Entity(repositoryClass="Customize\Repository\StoreEntryRepository")
     */
    class StoreEntry extends \Eccube\Entity\AbstractEntity
    {
        
        /**
         * @var int
         *
         * @ORM\Column(name="id", type="integer", options={"unsigned":true})
         * @ORM\Id
         * @ORM\GeneratedValue(strategy="IDENTITY")
         */
        private $id;

        /**
         * @var string
         *
         * @ORM\Column(name="name", type="string", length=255)
         */
        private $name;

        /**
         * @var string|null
         *
         * @ORM\Column(name="postal_code", type="string", length=8, nullable=true)
         */
        private $postal_code;

        /**
         * @var string|null
         *
         * @ORM\Column(name="addr01", type="string", length=255, nullable=true)
         */
        private $addr01;

        /**
         * @var string|null
         *
         * @ORM\Column(name="addr02", type="string", length=255, nullable=true)
         */
        private $addr02;

        /**
         * @var string|null
         *
         * @ORM\Column(name="phone_number", type="string", length=14, nullable=true)
         */
        private $phone_number;

        /**
         * @var string|null
         *
         * @ORM\Column(name="note", type="string", length=4000, nullable=true)
         */
        private $note;


        /**
         * @var \Eccube\Entity\Master\Pref
         *
         * @ORM\ManyToOne(targetEntity="Eccube\Entity\Master\Pref")
         * @ORM\JoinColumns({
         *   @ORM\JoinColumn(name="pref_id", referencedColumnName="id")
         * })
         */
        private $Pref;


        /**
         * Get id.
         *
         * @return Id
         */
        public function getId()
        {
            return $this->id;
        }

        
        /**
         * Get name
         *
         * @return name
         */
        public function getName()
        {
            return $this->name;
        }

        /**
         * Set shopname
         *
         * @return this
         */
        public function setName($name)
        {
            $this->name = $name;
            return $this;
        }
        
        /**
         * Set postal_code.
         *
         * @param string|null $postal_code
         * @return this
         */
        public function setPostalCode($postal_code = null)
        {
            $this->postal_code = $postal_code;
            return $this;
        }

        /**
         * Get postal_code.
         *
         * @return string|null
         */
        public function getPostalCode()
        {
            return $this->postal_code;
        }

        /**
         * Set addr01.
         *
         * @param string|null $addr01
         * @return this
         */
        public function setAddr01($addr01 = null)
        {
            $this->addr01 = $addr01;
            return $this;
        }

        /**
         * Get addr01.
         *
         * @return string|null
         */
        public function getAddr01()
        {
            return $this->addr01;
        }

        /**
         * Set addr02.
         *
         * @param string|null $addr02
         * @return this
         */
        public function setAddr02($addr02 = null)
        {
            $this->addr02 = $addr02;
            return $this;
        }

        /**
         * Get addr02.
         *
         * @return string|null
         */
        public function getAddr02()
        {
            return $this->addr02;
        }

        /**
         * Set phone_number.
         *
         * @param string|null $phone_number
         * @return this
         */
        public function setPhoneNumber($phone_number = null)
        {
            $this->phone_number = $phone_number;
            return $this;
        }

        /**
         * Get phone_number.
         *
         * @return string|null
         */
        public function getPhoneNumber()
        {
            return $this->phone_number;
        }


        /**
         * Get pref.
         *
         * @return \Eccube\Entity\Master\Pref|null
         */
        public function getPref()
        {
            return $this->Pref;
        }

        /**
         * Set pref.
         *
         * @param \Eccube\Entity\Master\Pref|null $pref
         * @return this
         */
        public function setPref(\Eccube\Entity\Master\Pref $pref = null)
        {
            $this->Pref = $pref;
            return $this;
        }


    }
}
```

\\app\\Customize\\Repository\\StoreEntryRepository.php
```php
<?php

namespace Customize\Repository;

use Customize\Entity\StoreEntry;
use Eccube\Repository\AbstractRepository;
use Eccube\Util\StringUtil;
use Symfony\Bridge\Doctrine\RegistryInterface;

/**
 * StoreEntryRepository
 *
 * This class was generated by the Doctrine ORM. Add your own custom
 * repository methods below.
 */
class StoreEntryRepository extends AbstractRepository
{
    public function __construct(RegistryInterface $registry)
    {
        parent::__construct($registry, StoreEntry::class);
    }
}
```


리포지토리, 엔티티 생성 후 
프록시,캐시 클리어, 디비 갱신 커맨드 실행
> php C:\xampp\htdocs\ec-cube\bin\console eccube:generate:proxies
> php C:\xampp\htdocs\ec-cube\bin\console cache:clear --no-warmup
> php C:\xampp\htdocs\ec-cube\bin\console eccube:schema:update --dump-sql --force


테이블 생성 완료
![[20220818-01.PNG]]

----
### 출처 :
-


### 연결메모
-














