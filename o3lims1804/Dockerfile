FROM ubuntu:18.04
MAINTAINER Joakim Lemstrom <joakim.lemstrom@bytewize.com>
RUN echo "tzdata tzdata/Areas select Europe" |debconf-set-selections
RUN echo "tzdata tzdata/Zones/Europe select Stockholm" |debconf-set-selections
RUN export DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true && apt update && apt -qqy install gcc make libcrypt-ssleay-perl libtext-autoformat-perl libmath-round-perl libmime-lite-perl libmime-tools-perl libio-zlib-perl libarchive-zip-perl libfile-which-perl libgd-text-perl libtemplate-perl ghostscript apache2 libapache2-mod-apreq2 libapache2-mod-perl2 libapache2-mod-perl2-dev libapache2-request-perl libgd-gd2-perl libgd-text-perl libdbi-perl libclass-dbi-mysql-perl libcompress-bzip2-perl libclass-accessor-perl libcompress-raw-zlib-perl libtext-reform-perl libtext-template-perl clamav clamav-daemon libclamav-client-perl libapache-dbi-perl libxml-writer-perl shared-mime-info libspreadsheet-parseexcel-simple-perl libimage-size-perl libdatetime-timezone-perl texlive texlive-latex-recommended texlive-extra-utils texlive-latex-extra imagemagick perlmagick libcairo-perl default-jre texlive-xetex lmodern cm-super cpanminus libtime-parsedate-perl libemail-valid-perl texlive-lang-european libexcel-writer-xlsx-perl
#RUN cpanm --self-upgrade
RUN cpanm YAML Test::Pod Test::Deep Test::Output Test::Exception MD5 SVG Math::SigFigs XML::Parser::Wrapper CGI::Apache2::Wrapper File::BaseDir File::DesktopEntry File::MimeInfo::Magic Math::Cephes MooseX::Aliases Class::MOP Moose DateTime::Locale DateTime File::Slurp LaTeX::Driver LaTeX::Encode LaTeX::Table Template::Latex DateTime DateTime::Duration Spreadsheet::SimpleExcel DateTime::Format::Excel Chart::Clicker JSON
# Net::AWS::SES - Problem att testa Net::AWS::SES, därför körs den nedan med -T
RUN cpan -T Net::AWS::SES

ADD includes/virtualhost_template_conf /etc/apache2/sites-available/o3.conf
RUN a2ensite o3.conf
RUN a2dissite 000-default
RUN a2enmod apreq2

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

#ENTRYPOINT ["/usr/sbin/apache2"]
#CMD ["-D", "FOREGROUND"]
EXPOSE 80
