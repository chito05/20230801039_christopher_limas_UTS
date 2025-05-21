# 20230801039_christopher_limas_UTS
uts keaman informasi
composer create-project laravel/laravel data-beasiswa
cd data-beasiswa
composer require filament/filament
php artisan filament:install
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate
use Spatie\Permission\Models\Role;

Role::create(['name' => 'admin']);
Role::create(['name' => 'staff']);
Role::create(['name' => 'student']);
Schema::create('beasiswas', function (Blueprint $table) {
    $table->id();
    $table->foreignId('user_id')->constrained()->onDelete('cascade');
    $table->string('jenis');
    $table->decimal('jumlah_dana', 10, 2);
    $table->enum('status', ['pending', 'approved', 'rejected']);
    $table->string('dokumen')->nullable(); // File PDF
    $table->timestamps();
});

$request->file('dokumen')->store('dokumen-beasiswa', 'private');
'disks' => [
    'private' => [
        'driver' => 'local',
        'root' => storage_path('app/private'),
        'visibility' => 'private',
    ],
],

public function view(User $user, Beasiswa $beasiswa)
{
    return $user->id === $beasiswa->user_id || $user->hasRole('admin');
}


protected $casts = [
    'dokumen' => 'encrypted',
];
