10/05/2021 - 14h15

# Padrões e Técnicas avançadas de Git e GitHub

* GitFlow;
* Configurações das branches;
* Pull Requests / Templates para PR;
* Code Review;
* Plugin do VSCode;
* CODEOWNERS;
* SemVer - Semantical Versioning;
* Conventional Commits;


# Iniciando com GitFlow

* Master/Main;
* Hotfix;
* Release;
* Develop;
* Feature/x;
* Feature/y;
* [GitHub GitFlow extension](https://github.com/petervanderdoes/gitflow-avh/wiki/Installation);

* $ git flow - mostra opções;
* $ git flow init - define nomes das branches e prefixo de tags;
* $ git flow feature start <feature_name>;
* $ git flow feature finish <feature_name> - faz merge na develop, remove a branch feat e
	faz checkout pra develop;
* $ git flow release start 0.1.0;
* $ git flow release finish 0.1.0 - faz merge no master, adiciona tag e faz merge no
	develop (caso haja mudança de última hora no branch release);
* $ git flow hotfix start <fix_name>;
* $ git flow hotfix finish <fix_name> - faz merge no master, cria uma nova tag e faz
	merge na develop;


# Assinatura de Commits

* Chaves privada e pública;
* apg-get install gpg;
* gpg --list-secret-key --keyid-form LONG;
* gpg --full-generate-key - default(1);
* gpg --armor --export <key_id>;
* Copia endereço gerado / GitHub / Configurações / SSH e GPG keys / add key;
* git config --global user.signingkey <key_id>;
* export GPG_TTY=$(tty) - add in nano ./bash_profile;
* git config commit.gpgsign true - assina somente um repositório;
* git config --global commit.gpgsign true - assina todos repositórios;
* git config --global commit.gpgSign true - assina tags;
* git log --show-signature -1;
* nano /.gnupg/gpg.conf / use-agent / CTRL+s / $ gpgconf --launch gpg-agent:
	- salva senha;
* gpg --edit-key <key_id> / $ adduid / name/email - adicionar novo e-mail na assinatura;
* $ uid 2 / trust / 5 / y / $ save;


# PRs e Codereview

* Protegendo branches:
		- main -> Settings/Branches -> Default Branch = Develop;
		- Branch protection rules -> add rule -> branch name pattern =  main (feature/*);
		- Check -> Include administrators, Restrict who can push to matching branches (people, team, apps);
		- Sobre proteção de branches e organizações
				O processo de proteção de branches que restringe quem poderá realizar o push é uma funcionalidade que está disponível apenas para repositórios associados a uma organização no Github (o que é o mais comum quando trabalhamos com github em uma empresa).
				Logo, se você não estiver vendo a opção: "Restrict who can push to matching branches" e quiser testar o recurso, crie uma organização no Github e crie um repositório associado a ela.

* Template pra PR:
		- [.github/PULL_REQUEST_TEMPLATE.md](https://github.com/embeddedartistry/templates/blob/master/.github/PULL_REQUEST_TEMPLATE.md)

* Code Review:
		- Start Review;
		- Outdated;
		- Approve;
		- Merge;
		- Protegendo branch para code review:
				+ Settings / branches / Check -> Require PR review before merging / number of people;
		- CODEOWNERS - explicitar quem pode fazer revisão (plano pago em projeto privado);
				+ file: CODEOWNERS:
						```
							*.js @some_user
							.github/ @other_user
							*.go @JuniorGunner
						```
				+ Settings / branches / Check -> Require review from Code Owners;
		- Extensão GitHub para VSCode;
				+ Show issues, PR's, etc;

# SEMVER e Conventional Commits

* [SEMVER](https://semver.org/)
* 2.1.4:
		- (2) MAJOR - Versão principal - API pública
		- (1) MINOR - Adicionou funcionalidades, mas compatível com a API (não quebra);
		- (4) PATCH - Bugs, ajustes;
		- MAJOR = 0 - API instável, pode mudar a qualquer momento;
		- 1.0.0-alpha(.beta, .rc0, .rc.1, .alpha.beta, etc) < 1.0.0

* [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
		- fix, feat, BREAKINGCHANGE, etc;
* Plugin VSCode - Conventional Commits;
* [Commitlint](https://commitlint.js.org/#/);
* [Commitsar](https://commitsar.tech/docs/);
* [Commitzen](https://github.com/commitizen/cz-cli) - plugin no terminal;
		+ Deixar repositório "commitzen friendly";
		+ ```$ git cz```;
